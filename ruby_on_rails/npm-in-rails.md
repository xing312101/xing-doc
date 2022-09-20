# npm-in-rails
> https://ricostacruz.com/til/npm-in-rails

```
1. version control ignore /node_modules
git:
echo '/node_modules' >> .gitignore
svn:
svn propset svn:ignore node_modules
or
svn propset svn:global-ignores node_modules

2.
create package.json and npm init
note: package.json is already in rails 5.

3. add node_modules to asset path
at config/application.rb
module YourApp
	class Application < Rails::Application
		config.assets.paths << Rails.root.join('node_modules')

note: the code is already in rails 5.

4. npm install
config/initializers/npm.rb:
system 'npm install' if Rails.env.development? || Rails.env.test?

5. add file to asset
//= require xxxxxxxxx
```
