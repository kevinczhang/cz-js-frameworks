# Multiple app project

Refer: [https://medium.com/disney-streaming/combining-multiple-angular-applications-into-a-single-one-e87d530d6527](https://medium.com/disney-streaming/combining-multiple-angular-applications-into-a-single-one-e87d530d6527)

Sample app is : D:\AngularWorkspace\sub-apps-setup-master

```
ng new MainProject --createApplication="false"
cd MainProject
ng generate application staff
ng generate application agent
ng generate application customer

ng build --prod --project="agent"
ng build --prod --project="staff"
ng build --prod --project="customer"
```

## Run the App <a href="#9c77" id="9c77"></a>

There are 3 ways to run the app.

1. `ng serve staff`
2. Use the project flag. `ng serve --project="staff" --port=4000`
3. Open the **angular.json** and locate the `defaultProject` at the bottom. Set it to `staff` and run `ng serve`.

## Injecting Sub Apps into Main application <a href="#b3cc" id="b3cc"></a>

In  **app.module.ts** from any one of our projects

```typescript
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

@NgModule({})
export class App1SharedModule{
  static forRoot(): ModuleWithProviders {
    return {
      ngModule: AppModule,
      providers: []
    }
  }
}
```

In Main Project app.module.ts

```typescript
imports: [
  BrowserModule,
  AppRoutingModule,
  App1SharedModule.forRoot(),
  App2SharedModule.forRoot()
],
```

