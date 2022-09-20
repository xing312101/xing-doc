# Http Server Interceptor

## generate interceptor
```
ng g interceptor interceptors/server-interceptor
```

## interceptor with handle auth
```
export class ServerInterceptor implements HttpInterceptor {
  constructor(private router: Router, private loadingService: LoadingService) { }

  intercept(request: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {
    let apiReq = request;

    return next.handle(apiReq).pipe(
      map(res => {
        if (res instanceof HttpResponse) {
        }
        else if (res instanceof HttpErrorResponse) {
          if (res.status === 401) {
            this.router.navigate(['/']);
          }
        }

        return res;
      })
    );
  }
}
```
