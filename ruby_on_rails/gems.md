# Gems
> 有些沒寫在這，基本上就是紀錄

## rerun
```
# in Gemfile
> it will listen project file and automatily restart rackup webserver

source 'https://rubygems.org'
group :development do
  gem 'rerun'
end

$ bundle install
$ bundle exec rerun -- rackup -p 3001

```