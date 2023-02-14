# Upgrade Rails
> https://guides.rubyonrails.org/upgrading_ruby_on_rails.html

## map.connect
```
# map.connect ':controller/:action/:id'
# map.connect ':controller/:action/:id.:format'

match ':controller/:action/:id', via: [:get, :post]
```

