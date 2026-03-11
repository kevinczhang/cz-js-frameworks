---
description: >-
  Component templates are not always fixed. An application may need to load new
  components at runtime.
---

# Dynamic Component

### The anchor directive <a href="#the-anchor-directive" id="the-anchor-directive"></a>

```typescript
import { Directive, ViewContainerRef } from '@angular/core';

@Directive({
  selector: '[ad-host]',
})
export class AdDirective {
  constructor(public viewContainerRef: ViewContainerRef) { }
}
```

### Loading components <a href="#loading-components" id="loading-components"></a>

```markup
template: `
            <div class="ad-banner-example">
              <h3>Advertisements</h3>
              <ng-template ad-host></ng-template>
            </div>
          `
```

### Resolving components <a href="#resolving-components" id="resolving-components"></a>

```typescript
export class AdBannerComponent implements OnInit, OnDestroy {
  @Input() ads: AdItem[];
  currentAdIndex = -1;
  @ViewChild(AdDirective, {static: true}) adHost: AdDirective;
  interval: any;

  constructor(private componentFactoryResolver: ComponentFactoryResolver) { }

  ngOnInit() {
    this.loadComponent();
    this.getAds();
  }

  ngOnDestroy() {
    clearInterval(this.interval);
  }

  loadComponent() {
    this.currentAdIndex = (this.currentAdIndex + 1) % this.ads.length;
    const adItem = this.ads[this.currentAdIndex];

    const componentFactory = this.componentFactoryResolver.resolveComponentFactory(adItem.component);

    const viewContainerRef = this.adHost.viewContainerRef;
    viewContainerRef.clear();

    const componentRef = viewContainerRef.createComponent(componentFactory);
    (<AdComponent>componentRef.instance).data = adItem.data;
  }

  getAds() {
    this.interval = setInterval(() => {
      this.loadComponent();
    }, 3000);
  }
}
```

&#x20;To ensure that the compiler still generates a factory, add dynamically loaded components to the [`NgModule`](https://angular.io/api/core/NgModule)'s `entryComponents` array:

### The Dynamic _AdComponent_ interface <a href="#the-adcomponent-interface" id="the-adcomponent-interface"></a>

{% tabs %}
{% tab title="ad.component.ts" %}
```typescript
export interface AdComponent {
  data: any;
}
```
{% endtab %}

{% tab title="hero-job-ad.component.ts" %}
```typescript
import { Component, Input } from '@angular/core';

import { AdComponent }      from './ad.component';

@Component({
  template: `
    <div class="job-ad">
      <h4>{{data.headline}}</h4>

      {{data.body}}
    </div>
  `
})
export class HeroJobAdComponent implements AdComponent {
  @Input() data: any;

}
```
{% endtab %}

{% tab title="hero-profile.component.ts" %}
```typescript
import { Component, Input }  from '@angular/core';

import { AdComponent }       from './ad.component';

@Component({
  template: `
    <div class="hero-profile">
      <h3>Featured Hero Profile</h3>
      <h4>{{data.name}}</h4>

      <p>{{data.bio}}</p>

      <strong>Hire this hero today!</strong>
    </div>
  `
})
export class HeroProfileComponent implements AdComponent {
  @Input() data: any;
}
```
{% endtab %}
{% endtabs %}
