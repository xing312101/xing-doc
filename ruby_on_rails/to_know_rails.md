# To know rails

## 1. build a gem
> rails is a gem
```
bundle gem xing_gem

// write some code

gem build x_rails.gemspec

gem install ./x_rails-0.1.0.gem

```
##### try in irb
```
require 'x_rails'  // include
XRails.who  // the function
```

## 2. generate gem commands
> like rails new app_name

create a file at project/bin
```
touch bin/hello
chmod a+x bin/hello
```

code
```
#!/usr/bin/env ruby

require 'x_rails'
puts XRails.hello(ARGV[0])
```

## 3. to know rack

#### if "rakcup" does not exist
```
gem install rackup
```

#### New a rack project/dir
new a config.rb file.
```
run proc{
    [200, {'content-type' => 'text/html'},
    ["Hello, YuXing!"]]
}
```

## 4. start an app

create the app project and struct
```
mkdir config
mkdir app
touch Gemfile
```

#### Add the gem into the Gemfile
```
source 'https://rubygems.org'
gem 'x_rails', path: "/Users/xing/workspace/xLearnRails/x_rails"
```

#### Add config.rb
```
run proc{
    [200, {'content-type' => 'text/html'},
    ["Hello, YuXing!"]]
}
```
