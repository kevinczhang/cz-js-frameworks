# Http and async

Example codes to be tested

{% tabs %}
{% tab title="auth.service.ts" %}
```typescript
export class AuthService {
    isAuthenticated(): Promise<boolean> {
        re
turn Promise.resolve(!!localStorage.getItem('token'));
    }
}
```
{% endtab %}

{% tab title="login.component.ts" %}
```typescript
import { Component } from '@angular/core';
import { AuthService } from "./auth.service";

@Component({
  selector: 'app-login',
  template: `
  <a>
    <span *ngIf="needsLogin">Login</span>
    <span *ngIf="!needsLogin">Logout</span>
  </a>
`
})
export class LoginComponent implements OnInit {

  needsLogin: boolean = true;

  constructor(private auth: AuthService) {
  }

  ngOnInit() {
    this.auth.isAuthenticated().then((authenticated) => {
      this.needsLogin = !authenticated;
    })
  }
}
```
{% endtab %}
{% endtabs %}

### `fakeAsync` and `tick`

```typescript
it('Button label via fakeAsync() and tick()', fakeAsync(() => { (1)
  expect(el.nativeElement.textContent.trim()).toBe('');
  fixture.detectChanges();
  expect(el.nativeElement.textContent.trim()).toBe('Login');
  spyOn(authService, 'isAuthenticated').and.returnValue(Promise.resolve(true));
  component.ngOnInit();

  tick(); (2)
  fixture.detectChanges();
  expect(el.nativeElement.textContent.trim()).toBe('Logout');
}));
```

1. &#x20;Like `async` we wrap the test spec function in a function called `fakeAsync`.
2. &#x20;We call `tick()` when there are pending asynchronous activities we want to complete.

The `tick()` function _blocks execution_ and simulates the passage of time until all pending asynchronous activities complete. So when we call `tick()` the application sits and waits for the promise returned from `isAuthenticated`to be resolved and then lets execution move to the next line.

{% hint style="info" %}
&#x20;`fakeAsync` does have some drawbacks, it doesn’t track XHR requests for instance.
{% endhint %}

### `async` and `whenStable`

```typescript
it('Button label via async() and whenStable()', async(() => { (1)
  fixture.detectChanges();
  expect(el.nativeElement.textContent.trim()).toBe('Login');
  spyOn(authService, 'isAuthenticated').and.returnValue(Promise.resolve(true));
  fixture.whenStable().then(() => { (2)
    fixture.detectChanges();
    expect(el.nativeElement.textContent.trim()).toBe('Logout');
  });
  component.ngOnInit();
}));
```

1. &#x20;We wrap our test spec function in another function called `async`.
2. &#x20;We place the tests we need to run after the `isAuthenticated` promise resolves inside this function.

This `async` function executes the code inside it’s body in a special _async test zone_. This intercepts and _keeps track_ of all promises created in it’s body. Only when all of those pending promises have been resolved does it then resolves the promise returned from `whenStable`.

## Testing Http

Code to be tested:

```typescript
import {Injectable} from '@angular/core';
import {Jsonp} from '@angular/http';
import 'rxjs/add/operator/toPromise';

class SearchItem {
  constructor(public name: string,
              public artist: string,
              public thumbnail: string,
              public artistId: string) {
  }
}

@Injectable()
export class SearchService {
  apiRoot: string = 'https://itunes.apple.com/search';
  results: SearchItem[];

  constructor(private jsonp: Jsonp) {
    this.results = [];
  }

  search(term: string) {
    return new Promise((resolve, reject) => {
      this.results = [];
      let apiURL = `${this.apiRoot}?term=${term}&media=music&limit=20&callback=JSONP_CALLBACK`;
      this.jsonp.request(apiURL)
          .toPromise()
          .then(
              res => { // Success
                this.results = res.json().results.map(item => {
                  console.log(item);
                  return new SearchItem(
                      item.trackName,
                      item.artistName,
                      item.artworkUrl60,
                      item.artistId
                  );
                });
                resolve(this.results);
              },
              msg => { // Error
                reject(msg);
              }
          );
    });
  }
}
```

Unit tests:

```typescript
it('search should return SearchItems', fakeAsync(() => { (1)
  let response = {
    "resultCount": 1,
    "results": [
      {
        "artistId": 78500,
        "artistName": "U2",
        "trackName": "Beautiful Day",
        "artworkUrl60": "image.jpg",
      }]
  };

  // When the request subscribes for results on a connection, return a fake response
  backend.connections.subscribe(connection => {
    connection.mockRespond(new Response(<ResponseOptions>{
      body: JSON.stringify(response)
    }));
  });

  // Perform a request and make sure we get the response we expect
  service.search("U2"); (2)
  tick(); (3)

  expect(service.results.length).toBe(1); (4)
  expect(service.results[0].artist).toBe("U2");
  expect(service.results[0].name).toBe("Beautiful Day");
  expect(service.results[0].thumbnail).toBe("image.jpg");
  expect(service.results[0].artistId).toBe(78500);
}));
```

1. &#x20;We use the `fakeAsync` method to execute in the special _fake async zone_ and track pending promises.
2. &#x20;We make the _asynchronous_ call to `service.search(…​)`
3. &#x20;We issue a `tick()` which blocks execution and waits for all the pending promises to be resolved.
4. &#x20;We now _know_ that the service has received and parsed the response so we can write some expectations.
