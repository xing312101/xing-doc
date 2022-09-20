# Angular Material
> https://material.angular.io/

> https://mateial.io/design/layout/responsive-layout-grid.html


## Veiwport
```
<meta name="viewport" content="width=device-width, initial-scale=1.0">

attributes:
width
height
initial-scale
minimum-scale
maximum-scale
user-scaleable

```

## install
> https://v6.material.angular.io/guide/getting-started

```
ng add @angular/material

ng add @angular/material@6
npm install --save @angular/cdk@6


npm install --save @angular/material @angular/cdk

ng add material-design-icons
or
in style.css
@import 'https://fonts.googleapis.com/icon?family=Material+Icons';

```

## @angular/animations
```
npm install --save @angular/animations
```


#### let all browser supported
```
npm install --save web-animations-js
```

## HammerJS
```
npm install --save hammerjs
```

## SideNav
```
import { MatSidenavModule } from '@angular/material/sidenav'


<mat-sidenav-container>
<mat-sidenav>
<mat-sidenav-content>
```

#### template
```
Ex:
<mat-sidenav-container>
    <mat-sidenav>
    </mat-sidenav>

    <mat-sidenav-content>
        <button mat-button>Hello</button>
        <router-outlet></router-outlet>
    </mat-sidenav-content>
</mat-sidenav-container>

```

#### Toggle mat-sidenv
```
toggleSideNav(sideNav: MatSidenav) {
    sideNav.toggle().then((result: MatDrawerToggleResult) => {
    console.log("toggle");
    });
}
```

## Mat-Drawer
it is like sideNav
```
<mat-drawer-container>
    <mat-drawer>
    </mat-drawer>
    <mat-drawer-content>
    </mat-drawer-content>
</mat-drawer-container>
```


## MatToolbar
```
import { MatToolbarModule } from '@angular/material/toolbar'


<mat-toolbar>
    Tool Bar
</mat-toolbar>
```

#### fixed tool bar
```
/* css */
.app-toolbar {
    position: fixed;
    top: 0;
    z-index: 2;
}

.app-toolbar-seprator {
    flex: 1 1 auto;
}

.app-container,
.app-sidenav {
    position: absolute;
    padding-top: 64px; /* min: tool-bar height */
    height: calc(100vh - 64px);

}

ex:
<mat-toolbar class="app-toolbar">
    <button mat-icon-button (click)="sideNav.toggle()">
        <mat-icon>{{sideNav.opened ? 'close' : 'menu'}}</mat-icon>
    </button>

    <span class="toolbar-seprator"></span>

    <button>this is right button</button>

</mat-toolbar>
<mat-sidenav-container class="app-container">
    <mat-sidenav class="app-sidenav">
    </mat-sidenav>

    <mat-sidenav-content>
        <button mat-button>Hello</button>
        <router-outlet></router-outlet>
    </mat-sidenav-content>
</mat-sidenav-container>

```

## MatList
```
<mat-list>
<mat-list-item>

<mat-nav-list>

<mat-divider>

matSubheader
matLine
matListAvatar

<mat-selection-list>
    <mat-list-option>
    </mat-list-option>
</mat-selection-list>
```

## MatMenuModule
```
<mat-menu #msgMeue="matMenu">
    <button mat-menu-item>hello 1</button>
    <button mat-menu-item [matMenuTriggerFor]="hello another menu">hello level 2</button>
</mat-menu>

<button mat-icon-button [matMenuTriggerFor]="msgMenu" #menuTrigger="matMenuTrigger">
    <mat-icon>message</mat-icon>
</button>


```

## MatStep


## MatInput

#### autocomplete


## MatDatepicker

## MatSelect

## mat-form-field
#### float label
#### placeholder
#### mat-hint
#### mat-error
#### matPrefix MatSuffix

## mat-checkbox
## mat-radio-button
## mat-slide-toggle
## mat-slider


## mat-gridlist
```
import {MatGridListModule} from '@angular/material/grid-list';
```
#### mat-grid-list
#### mat-grid-tile


## mat-card

## mat-progress-bar mat-progress-spinner

## Dialog
> https://material.angular.io/components/dialog

#### dialog service
```
export class DialogService {
  constructor(public dialog: MatDialog) { }

  public openDialog() {
    const dialogRef = this.dialog.open(targetComponent, {
      data: {
        hello: "world"
      },
      height: "calc(100%) - 10px",
      width: "calc(100%) - 10px",
      maxWidth: "100%",
      maxHeight: "100%"
    });

    dialogRef.afterOpen().subscribe(r => {
      console.log("after open");
    });
    dialogRef.beforeClose().subscribe(r => {
      console.log("before close");
    });
    dialogRef.afterClosed().subscribe(r => {
      console.log("after closed");
    });
  }
}

```

#### open dialog component
```
import { MatDialogModule } from '@angular/material/dialog'

export class AppComponent
  constructor(private dialogService: DialogService) { }
  openDialog() {
    this.dialogService.openDialog();
  }
}
```

## mat-chip matTooltip matSnackBar


## mat-expansion-panel

## mat-tab


## mat-table
```
import { MatTableModule } from '@angular/material/table'
```

## MatIconModule
```
import { MatIconModule } from '@angular/material/icon'
```

## CDK Bidirectionlity

## CDK Ibservables

## CDK Scrolling

## CDK cdkPortalOutlet

## CDK Overlay

## CDK breakpoint



## using at tool bar
.toolbar-seprator {
  flex: 1 1 auto;
}


## custom theme
> https://materialpalette.com
> http://mcg.mbitson.com/

create themes/your-theme.scss
```
@import '~@angular/material/theming';
@include mat-core();

$md-mcgpalette0: (
    50 : #e1e7ed,
    100 : #b3c2d1,
    200 : #819ab3,
    300 : #4f7295,
    400 : #29537e,
    500 : #033567,
    600 : #03305f,
    700 : #022854,
    800 : #02224a,
    900 : #011639,
    A100 : #6f96ff,
    A200 : #3c71ff,
    A400 : #094bff,
    A700 : #0040ef,
    contrast: (
        50 : #000000,
        100 : #000000,
        200 : #000000,
        300 : #ffffff,
        400 : #ffffff,
        500 : #ffffff,
        600 : #ffffff,
        700 : #ffffff,
        800 : #ffffff,
        900 : #ffffff,
        A100 : #000000,
        A200 : #ffffff,
        A400 : #ffffff,
        A700 : #ffffff,
    )
);

$custom-primary: mat-palette($md-mcgpalette0, 600);
$custom-accent: mat-palette($mat-teal);
$custom-warn: mat-palette($mat-deep-orange);
$custom-theme: mat-light-theme($custom-primary, $custom-accent, $custom-warn);

@include angular-material-theme($custom-theme);


```





