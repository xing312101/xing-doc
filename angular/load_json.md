# load json
> https://www.techiediaries.com/angular-local-json-files/

## Method 1: Reading Local JSON Files Using TypeScript 2.9+ import Statement

supported only in Angular 6.1+ versions.
```
import { Component, OnInit } from '@angular/core';
import * as data from './data.json';

@Component({
  selector: 'app-root',
  template: `<ul>
      <li *ngFor="let product of products">

      </li>
  </ul>`,
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  title = 'Angular Example';

  products: any = (data as any).default;

  constructor(){}
  ngOnInit(){
    console.log(data);
  }
}
```

## Method 2: Reading Local JSON Files Using Angular HttpClient

#### import HttpClientModule first
```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';

import { AppComponent } from './app.component';


@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    AboutComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

#### Using
```
import { Component, OnInit } from '@angular/core';
import { HttpClient } from "@angular/common/http";


@Component({
  selector: 'app-root',
  template: `<ul>
      <li *ngFor="let product of products">

      </li>
  </ul>`,
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  title = 'Angular Example';
  products: any = [];

  constructor(private httpClient: HttpClient){}
  ngOnInit(){
    this.httpClient.get("assets/data.json").subscribe(data =>{
      console.log(data);
      this.products = data;
    })
  }
}
```

## Method 3: Reading Local JSON Files in Offline Angular Apps Using ES6+ import Statement
```
declare module "*.json" {
  const value: any;
  export default value;
}
```
```
import * as data from "data.json";
```

