# AuthGuard
> ref: https://pvt5r486.github.io/f2e/20190609/1487025750/

## generate guard
```
ng generate guard auth/auth
```

## auth.guard.ts with httpService check
```
import { Injectable } from '@angular/core';
import { ActivatedRouteSnapshot, CanActivate, Router, RouterStateSnapshot, UrlTree } from '@angular/router';
import { map, Observable } from 'rxjs';
import { UserModel } from '../models/user-model';
import { AuthService } from '../services/auth.service';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(
    private authService: AuthService, private router: Router) { }
  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {

    return this.authService.checkUser().pipe(
      map((value) => {
        let user = new UserModel().deserialize(value);
        let isSame = false;
        let someData = sessionStorage.getItem('someData');

        if (someData == user.someData) {
          AuthService.setCurrentUser(user);
          isSame = true;
        } else {
          this.router.navigate(['/']);
        }

        return isSame;
      })
    );


  }
}
```


## app-routing.module.ts
```
const routes: Routes = [
  { path: '', redirectTo: '/login', pathMatch: 'full' },
  { path: 'list', component: ListComponent, canActivate: [AuthGuard], },
  { path: 'login', component: LoginComponent }
  // TODO: 404 page
];
```





