# To know rails

> ref: https://ithelp.ithome.com.tw/users/20065841/ironman/3021
> https://github.com/rails/rails

## 1. build a gem
> rails is a gem
```
bundle gem xing_gem // using 'x_rails' which means xing's rails to practice.

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

#### add dependency to x_rails
In x_rails/x_rails.gemspec
add rack dependency to mean x_rails is using rack framework.
```
spec.add_runtime_dependency "rack"
```

if use rspec
```
gem.add_development_dependency "rspec"
```


## 4. start an x_rails app

create the app project and struct
```
mkdir config
mkdir app
touch Gemfile
```

#### Add the gem into the Gemfile
```
source 'https://rubygems.org'
gem 'x_rails', path: "/Users/xing/xImitateRails/x_rails"
```

#### Add config.rb
```
run proc{
    [200, {'content-type' => 'text/html'},
    ["Hello, YuXing!"]]
}
```


## 5. Add application in x_rails

at module XRails in x_rails
```
  class Application
    def call(env)
      [200, {'content-type' => 'text/html'},
       ["I use XRails, GO!!!!"]]
    end
  end
```

at x_ror/config/application.rb in x_ror
```
require "x_rails"

module XRor
  class Application < XRails::Application
  end
end
```

at x_ror/config.ru
```
require_relative 'config/application'
run XRor::Application.new
```

## 6. controller and routing

#### routing.rb
create routing.rb at lib in x_rails
```
module XRails
  class Application
    def controller_and_action(env)
      before, controller, action, after = env["PATH_INFO"].split('/', 4)

      controller = controller.capitalize + "Controller"

      [Object.const_get(controller), action]
    end
  end
end
```

#### x_rails.rb
add routing to get controller and action
```
  class Application
    def call(env)
      # get controller name and action name
      klass, action =  get_controller_and_action(env)
      controller = klass.new(env)
      text = controller.send(action)

      [200,
        {'content-type' => 'text/html'},
        [text]
      ]
    end
  end

  class Controller
    attr_reader :env

    def initialize(env)
      @env = env
    end
  end
```


#### try using controller in x_ror
new a controller at app/controllers that same as rails

tasks_controller.rb
```
class TasksController < XRails::controller
  def index
    "Hello, there are tasks."
  end
end
```


#### add autoload method in config/application.rb
for auto reload file when refresh page
```
$LOAD_PATH << File.join(File.dirname(__FILE__), "..", "app", "controllers")
```
