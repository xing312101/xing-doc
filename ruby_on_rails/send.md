# send
```
class HelloWorld
	def hello
		puts "world"
	end
end

obj = HelloWorld.new
obj.send(:hello)
```
