# url encode
```
require 'uri'

URI.encode("Hello there world")
#=> "Hello%20there%20world"
URI.encode("hello there: world, how are you")
#=> "hello%20there:%20world,%20how%20are%20you"

URI.decode("Hello%20there%20world")
#=> "Hello there world"

URI.escape(s_target_url)
CGI::escape(s_target_url)
```
