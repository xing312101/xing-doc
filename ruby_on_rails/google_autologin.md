# Google AutoLogin
```
require 'net/http'
require 'net/https'
require 'cgi'
require 'uri'
require 'rubygems'
require 'hpricot'

module Net
	class HTTPS < HTTP
		def initialize(address, port = nil)
			super(address, port)
			self.use_ssl = true
		end
	end
end

class GAuth
	GOOGLE_LOGIN_URL = URI.parse('https://www.google.com/accounts/ServiceLoginBoxAuth')
	attr_reader :service, :url,:cookie

	def initialize(service,url)
		@service = service
		@url = url
	end

	def authenticate(email, password)
		$VERBOSE = nil
		response = Net::HTTPS.post_form(GOOGLE_LOGIN_URL,
			{'Email' => email,
			'Passwd' => password,
			'service' => service })

		@cookie = response.response["set-cookie"]

		response.error! unless response.kind_of? Net::HTTPSuccess

		@headers = {
			'Cookie' => @cookie
		}
	end

	def get(path)
		response, data = http.get(path, @headers)
		data
	end

	def http
		conn = Net::HTTP.new(url, 80)
		#conn.set_debug_output $stderr
		conn
	end
end

g = GAuth.new("blah","blah.google.com")
g.authenticate("blah@gmail.com","blah")
```
