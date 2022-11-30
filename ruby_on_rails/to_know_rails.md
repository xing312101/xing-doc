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


## 5. Using application in x_rails

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
class TasksController < XRails::Controller
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


## 7. Favicon and Homepage
#### x_rails
```
class Application
    def call(env)
      return favicon if '/favicon.ico' == env["PATH_INFO"]
      return index if '/' == env["PATH_INFO"]

      begin
        # get controller name and action name
        klass, action =  get_controller_and_action(env)
        controller = klass.new(env)
        text = controller.send(action)

        [200,
          {'content-type' => 'text/html'},
          [text]
        ]
      rescue
        [404, {'content-type' => 'text/html'},
        ['This is a 404 page!!']]
      end
    end

    private

    def index
      begin
        home_klass = Object.const_get('HelloController')
        controller = home_klass.new(env)
        text = controller.send(:index)
        [200, {'content-type' => 'text/html'}, [text]]
      rescue NameError
        [200, {'content-type' => 'text/html'}, ['This is a index page']]
      end
    end

    def favicon
      return [404, {'content-type' => 'text/html'}, []]
    end
  end
```
#### x_ror
add a HelloController
add require 'hello_controller'

## 8. autoload contorller

### $LOAD_PATH
It means that the library is there.

### $LOADED_FEATURES
It records the required library.

### const_missing
using const_missing to find which file need auto loading

at lib/x_rails/support.rb
```
class Object
  def self.const_missing(const)
    require XRails.to_underscore(const.to_s)
    Object.const_get(const)
  end
end
```

at lib/x_rails/dependencies.rb
```
class Object
  def self.const_missing(const)
    require XRails.to_underscore(const.to_s)
    FinalObject.const_get(const)
  end
end

class FinalObject < Object
  # avoid to unlimit loop
  def self.const_missing(const)
    nil
  end
end
```

in lib/x_rails.rb
```
require "x_rails/support"
require "x_rails/dependencies"
```

remove the request controller at x_ror/config


## View

### erubi
rails 5 ~ ... are using erubi not erb
```
## x_rails/x_rails.gemspec

spec.add_runtime_dependency "erubi"
```

```
gem 'erubi'
```

### controller class
create a controller.rb in lib/x_rails/

in lib/x_rails.rb
```
require "x_rails/controller"

remove the class controller code.
```

#### add render method and controller_name in controller.rb
```
def render(view_name)
    # project/app/views/{{controller_name}}/{{view_name}}.html.erb
    # the path as a convention
    filename = File.join "app", "views", controller_name, "#{view_name}.html.erb"
    viewTemplate = File.read filename
    eval(Erubi::Engine.new(viewTemplate).src)
end

def controller_name
    klass = self.class
    klass = klass.to_s.gsub /Controller$/, ""
    XRails.to_underscore klass
end
```

#### apply the view in x_ror
in TasksController
```
def index
    @message = "Hello YuXing, how about the view?"
    render('index')
end
```

create a view file: index.html.erb
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Index</title>
  </head>
  <body>
    <h1>task index page</h1>
    <%= @message %>
  </body>
</html>
```
