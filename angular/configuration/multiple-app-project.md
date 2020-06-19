# Multiple app project

```text
ng new MainProject --createApplication="false"
cd MainProject
ng generate application staff
ng generate application agent
ng generate application customer

ng build --prod --project="agent"
ng build --prod --project="staff"
ng build --prod --project="customer"
```

## Run the App <a id="9c77"></a>

There are 3 ways to run the app.

1. `ng serve staff`
2. Use the project flag. `ng serve --project="staff" --port=4000`
3. Open the **angular.json** and locate the `defaultProject` at the bottom. Set it to `staff` and run `ng serve`.

