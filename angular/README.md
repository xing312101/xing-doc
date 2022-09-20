# Angular
> https://angular.io/


## install
```
$ vim .nvmrc

npm install -save @angular/common@7 @angular/compiler@7 @angular/core@7 @angular/forms@7 @angular/platform-browser@7 @angular/platform-browser-dynamic@7 @angular/router@7 core-js@3 rxjs@6 zone.js@0

or
npm install -g @angular/cli

or specific version
npm i @angular/cli@6.2.4
```

## create
```
ng new projectName --directory ./

or

./node_modules/@angular/cli/bin/ng new project-name --directory ./
```

## commands
> https://angular.io/cli/generate#library-command

```
ng lint
ng test
ng build --prod
```
## bootstrap
```
npm install bootstrap jquery popper.js --save
```

## angular subrouter
> ref: https://appdividend.com/2018/12/14/angular-7-routing-and-sub-routing-tutorial-with-example/

```
ng g module moduleName
ng g c moduleName/category1
ng g c moduleName/category2
```

## ng-select
> ref: https://github.com/ng-select/ng-select

```
npm install --save @ng-select/ng-select
```

## angular 7 cdk drag-drop
> ref: https://material.angular.io/cdk/drag-drop/api

```
npm install @angular/cdk@7
```

## angular proxy
> https://medium.com/@spencerfeng/setup-a-proxy-for-api-calls-for-your-angular-cli-app-6566c02a8c4d


## interceptor
> https://wellwind.idv.tw/blog/2017/10/29/angular-advanced-handle-http-request-with-interceptor/


## Blob download file
```
service:
    const options = { responseType: 'blob' as 'json' };
    return this.http.get<Blob>(this.url, options);

component:
    this.userService.exportUsers().subscribe((res: Blob) => {
      console.log('exportUserList res:', res);

    }

```


## TODO: Think about SharedModule



## Fetch html element
```
@ViewChild("elementHtmlId", {static: true}) elementName: any;
// if do ocus()
this.elementName.nativeElement.focus();
```

## safe url
```
export class className {
  safeUrl: SafeUrl;

  constructor(private domSanitizer: DomSanitizer) {
    this.safeUrl = this.domSanitizer.bypassSecurityTrustUrl(stringUrl);
  }
}
```

## select element in component
```
constructor(private viewElem: ElementRef) {
    let targets = this.viewElem.nativeElement.querySelectorAll('.cssClassOrId');
}

```

