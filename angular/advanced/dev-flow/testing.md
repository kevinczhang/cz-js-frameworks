---
description: The CLI takes care of Jasmine and Karma configuration for you.
---

# Testing

&#x20;You can fine-tune many options by editing the `karma.conf.js` and the `test.ts` files in the `src/` folder.

## Testing services with the _TestBed_

&#x20;The `TestBed` is the most important of the Angular testing utilities. The `TestBed` creates a dynamically-constructed Angular _test_ module that emulates an Angular @NgModule.

&#x20;The `TestBed.configureTestingModule()` method takes a metadata object that can have most of the properties of an @NgModule.

```typescript
let service: ValueService;

beforeEach(() => {
  TestBed.configureTestingModule({ providers: [ValueService] });
});
```

&#x20;To test a service, you set the `providers` metadata property with an array of the services that you'll test or mock.

```typescript
it('should use ValueService', () => {
  service = TestBed.inject(ValueService);
  expect(service.getValue()).toBe('real value');
});
```

Or inside the `beforeEach()` if you prefer to inject the service as part of your setup.

```typescript
content_copybeforeEach(() => {
  TestBed.configureTestingModule({ providers: [ValueService] });
  service = TestBed.inject(ValueService);
});
```

&#x20;When testing a service with a dependency, provide the mock in the `providers` array.

```typescript
let masterService: MasterService;
let valueServiceSpy: jasmine.SpyObj<ValueService>;

beforeEach(() => {
  const spy = jasmine.createSpyObj('ValueService', ['getValue']);

  TestBed.configureTestingModule({
    // Provide both the service-to-test and its (spy) dependency
    providers: [
      MasterService,
      { provide: ValueService, useValue: spy }
    ]
  });
  // Inject both the service-to-test and its (spy) dependency
  masterService = TestBed.inject(MasterService);
  valueServiceSpy = TestBed.inject(ValueService) as jasmine.SpyObj<ValueService>;
});
```

## Testing HTTP services

```typescript
let httpClientSpy: { get: jasmine.Spy };
let heroService: HeroService;

beforeEach(() => {
  // TODO: spy on other methods too
  httpClientSpy = jasmine.createSpyObj('HttpClient', ['get']);
  heroService = new HeroService(<any> httpClientSpy);
});

it('should return expected heroes (HttpClient called once)', () => {
  const expectedHeroes: Hero[] =
    [{ id: 1, name: 'A' }, { id: 2, name: 'B' }];

  httpClientSpy.get.and.returnValue(asyncData(expectedHeroes));

  heroService.getHeroes().subscribe(
    heroes => expect(heroes).toEqual(expectedHeroes, 'expected heroes'),
    fail
  );
  expect(httpClientSpy.get.calls.count()).toBe(1, 'one call');
});

it('should return an error when the server returns a 404', () => {
  const errorResponse = new HttpErrorResponse({
    error: 'test 404 error',
    status: 404, statusText: 'Not Found'
  });

  httpClientSpy.get.and.returnValue(asyncError(errorResponse));

  heroService.getHeroes().subscribe(
    heroes => fail('expected an error, not heroes'),
    error  => expect(error.message).toContain('test 404 error')
  );
});
```

## Component class testing

```typescript
beforeEach(() => {
  TestBed.configureTestingModule({
    // provide the component-under-test and dependent service
    providers: [
      WelcomeComponent,
      { provide: UserService, useClass: MockUserService }
    ]
  });
  // inject both the component and the dependent service.
  comp = TestBed.inject(WelcomeComponent);
  userService = TestBed.inject(UserService);
});
```

### Component DOM testing <a href="#component-dom-testing" id="component-dom-testing"></a>

```typescript
describe('BannerComponent (minimal)', () => {
  it('should create', () => {
    TestBed.configureTestingModule({
      declarations: [ BannerComponent ]
    });
    const fixture = TestBed.createComponent(BannerComponent);
    const component = fixture.componentInstance;
    expect(component).toBeDefined();
  });
});
```

#### _nativeElement_ <a href="#nativeelement" id="nativeelement"></a>

```typescript
it('should have <p> with "banner works!"', () => {
  const bannerElement: HTMLElement = fixture.nativeElement;
  const p = bannerElement.querySelector('p');
  expect(p.textContent).toEqual('banner works!');
});
```

