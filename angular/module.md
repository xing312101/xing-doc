# module

## create module
```
ng generate module module_name
ng generate module module_name --routing=true
```

## create component in module
```
ng generate component componet_name --module module_name
```

## about route
loadChildren // 延遲載入
preloadingStrategy // 預先載入

## route config in root route
  {
    path: 'module_name',
    loadChildren: () => import('./module_name/module_name-routing.module').then(m => m.ModuleNameRoutingModule)
  }

