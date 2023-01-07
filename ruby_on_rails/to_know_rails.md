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


## 9. View

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

### helper
> ... 應該有更好的位置，目前先放controller

```
def link_to(name = nil, url = nil)
  "<a href=\"#{url}\">#{name}</a>"
end
```

### layout
先將原本的render的結果放到一個class的attribute
再做一個另一個像render的layout即可完成

at controller.rb in x_rails
```
attr_reader :content

def layout_render()
  filename = File.join("app", "views", "layouts", "application.html.erb")
  template = File.read(filename)
  eval(Erubi::Engine.new(template).src)
end

def content
  @content
end
```

layout file in x_ror
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Index</title>
  </head>
  <body>
    <div>
      Hello this is application layout.
    </div>
    <%= @content %>
  </body>
</html>
```

## 10. Model

### multi_json
> as db data
```
## x_rails/x_rails.gemspec

spec.add_runtime_dependency "multi_json"
```

### file_model
an like ActiveModel
```
## x_rails/lib/x_rails/file_model.rb

require "multi_json"

module XRails
  module Model
    class FileModel
      def initialize(file)
        @file = file
        basename = File.split(file)[-1]
        @id = File.basename(basename, ".json").to_i

        obj = File.read(file)
        @hash = MultiJson.load(obj)
      end

      def [](name)
        @hash[name.to_s]
      end

      def []=(name, value)
        @hash[name.to_s] = value
      end

      def self.find(id)
        begin
         FileModel.new("db/tasks/#{id}.json")
        rescue
         return nil
        end
      end
    end
  end
end
```

at x_rails/lib/x_rails.rb
```
require_relative "x_rails/file_model"
```

### Using in x_ror

#### create a db json
db/tasks/1.json
```
{
  "title": "第一個Task",
  "content": "吃喝拉撒睡"
}

```

#### def show method in tasks_controller
```
@task = Mavericks::Model::FileModel.find(1)
```

#### show.html.erb
```
<div style="padding: 20px; background: red;">
  <div style="padding: 5px; background: green;">
    <%= @task["title"] %>
  </div>
  <div style="padding: 5px; background: yellow;">
    <%= @task["content"] %>
  </div>
</div>
```

### model all data

#### def all in file_model
```
def self.all
  files = Dir['db/tasks/*.json']
  files.map { |f| FileModel.new f}
end
```

#### index.html.erb
```
<h1>任務的index</h1>
<%= @message %>
<%= link_to("task detail", "https://www.google.com/") %>

<% @tasks.each do |task| %>
  <div style="padding: 5px; background: red;">
    <div style="padding: 5px; background: green;">
      <%= task["title"] %>
    </div>
    <div style="padding: 5px; background: yellow;">
      <%= task["content"] %>
    </div>
  </div>
<% end %>
```

### model create record
#### def create in model
```
def self.create(attr)
  hash = {}
  hash[:title] = attr[:title]
  hash[:content] = attr[:content]

  # find max id
  id =  Dir['/Users/yuxinglee/xing/x_ror/db/tasks/*'].max[/\d+/]

  id = id ? id.to_i + 1 : 1

  File.open("db/tasks/#{id}.json", "w") do |f|
    f.write <<-TEMPLATE
      {
        "title": "#{hash[:title]}",
        "content": "#{hash[:content]}"
      }
    TEMPLATE
  end

    FileModel.new "db/tasks/#{id}.json"
end
```

#### def create in action
```
def create
  attrs = {
    title: 'Hello',
    content: 'Create a new record'
  }

  XRails::Model::FileModel.create(attrs)
  @tasks = XRails::Model::FileModel.all
  render 'index'
end
```


## 11. request

### x_rails controller handle "request"
```
def request
  @request || @request = Rack::Request.new(@env)
end

def params
  request.params
end
```

### Try params in show
```
def show
  @task = FileModel.find(params['id'])
end
```

## 12. response

#### x_rails controller handle "response"
```
def response(text, status = 200, headers = {})
  raise "Already responded!" if @response
  @response = Rack::Response.new(text, status, headers)
end

def get_response
  @response
end
```

#### Modify the response
remove isRendered
```
def call(env)
  return favicon if '/favicon.ico' == env["PATH_INFO"]
  return index(env) if '/' == env["PATH_INFO"]

  begin
    # get controller name and action name
    klass, action = get_controller_and_action(env)
    controller = klass.new(env)

    controller.send(action)
    default_render(controller, action) unless controller.content

    # layout
    controller.layout_render

    if controller.get_response
      controller.get_response.to_a
    else
      [500, {'Content-Type' => 'text/html'},
        ['server error!!']]
    end
  rescue => e
    puts e.message
    puts e.backtrace
    [404, {'content-type' => 'text/html'},
    ['This is a 404 page!!']]
  end
end
```

## 13. Migration

### Using SQLite
```
## x_rails/x_rails.gemspec
spec.add_runtime_dependency 'sqlite3'
```

### create a migration_file
#### migration_20221206.rb in x_ror
```
require 'sqlite3'

conn = SQLite3::Database.new "x_ror.db"

conn.execute <<SQL
create table tasks(
id INTEGER PRIMARY KEY,
title TEXT,
content TEXT);
SQL
```

RUN: $ bundle exec ruby hello_x_ror.rb


### SQLite model
x_rails/lib/x_rails/sqlite_model.rb
```
require 'SQLite3'

DB = SQLite3::Database.new 'x_ror.db'

module XRails
  module Model
    class SQLite
      def self.table
        table_name = XRails.to_underscore name
        XRails.to_plural table_name
      end

      def self.schema
        return @schema if @schema
        @schema = {}

        DB.table_info(table) do |row|
          @schema[row["name"]] = row["type"]
        end
        @schema
      end

    end
  end
end
```

##### to_plural
```
def self.to_plural(string)
  pattern = /.*s$|x$|z$|sh$|ch$/
  pattern.match?(string) ? "#{string}es" : "#{string}s"
end
```

#### get table schema
```
require 'x_rails/sqlite_model'
require 'x_rails/support'

class Task < XRails::Model::SQLite
end

puts Task.schema
```

## 14. ORM
### Create

```
class SQLite
  def initialize(data = nil)
    @hash = data
  end

  def self.to_safe_sql_string(val)
    case val
    when Numeric
      val.to_s
    when String
      "'#{val}'"
    else
      raise "Can't support #{val.class} to SQL!"
    end
  end

  def self.table
    table_name = XRails.to_underscore name
    XRails.to_plural table_name
  end

  def self.schema
    return @schema if @schema
    @schema = {}

    DB.table_info(table) do |row|
      @schema[row["name"]] = row["type"]
    end
    @schema
  end

  def self.create(values)
    values.delete :id
    keys = schema.keys - ['id']
    vals = keys.map do |key|
      values[key.to_sym] ? to_safe_sql_string(values[key.to_sym]) : "null"
    end

    DB.execute <<-SQL
      INSERT INTO #{table} (#{keys.join ","})
      VALUES (#{vals.join ","});
    SQL

    data = Hash[keys.zip values.values]
    sql = "SELECT last_insert_rowid();"
    data["id"] = DB.execute(sql)[0][0]
    self.new data
  end

  def self.count
    DB.execute(<<-SQL)[0][0]
      SELECT COUNT(*) FROM #{table}
    SQL
  end
end
```

### find & all
```
def self.find(id)
  row = DB.execute <<-SQL
    select #{schema.keys.join ","} from #{table}
    where id = #{id};
  SQL

  data = Hash[schema.keys.zip row[0]]
  self.new data
end

def self.all
  row = DB.execute <<-SQL
    select #{schema.keys.join ","} from #{table}
  SQL

  row.map do |attr|
    data = Hash[schema.keys.zip attr]
    self.new data
  end
end
```

### get & set
```
def [](name)
  @hash[name.to_s]
end

def []=(name, value)
  @hash[name.to_s] = value
end
```

### save & save!
```
def save!
  unless @hash["id"]
    self.class.create(@hash)
    return true
  end

  fields = @hash.map { |key, value| "#{key}=#{self.class.to_safe_sql_string(value)}" }.join ","

  DB.execute <<-SQL
    UPDATE #{self.class.table}
    SET #{fields}
    WHERE id = #{@hash["id"]}
  SQL

  true
end

def save
  self.save! rescue false
end
```

### delete
```
def delete
  unless @hash["id"]
    return true
  end

  DB.execute <<-SQL
    DELETE FROM #{self.class.table}
    WHERE id = #{@hash["id"]}
  SQL

  true
end
```

#### try script
```
require 'x_rails/sqlite_model'
require 'x_rails/support'

class Task < XRails::Model::SQLite

end

puts Task.schema

Task.create('title': 'Task', 'content': 'Smile')

puts Task.count

Task.all.each { |task| puts "#{task['title']} : #{task['content']}"  }

puts Task.find(1)['content']

Task.all.each { |task| task.delete }
```

## 15. attr_accessor

```
def method_missing(attr, *args)
  attrs = self.class.schema
  attr = attr.to_s.gsub('=', '')
  if attrs.key?(attr)
    self.class.define_attr(attrs)
    val = args.empty? ?  self.send(attr) : self.send("#{attr}=", args[0])
    return val
  else
    super
  end
end

def self.define_attr(attrs)
  attrs.keys.each do |attr|
    add_method_to_get(attr)
    add_method_to_set(attr)
  end
end

def self.add_method_to_get(attr)
  define_method attr do
    self[attr.to_s]
  end
end

def self.add_method_to_set(attr)
  define_method "#{attr}=" do |arg|
    self[attr.to_s] = arg
  end
end
```

## 16. powerful ORM
> using postgresql as db






