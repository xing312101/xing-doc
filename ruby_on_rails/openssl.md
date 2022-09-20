# OpenSSL
```
uri = URI.parse(url)
if (443 == uri.port)
	http = Net::HTTP.new(uri.host, uri.port)
	http.use_ssl = true
	http.verify_mode = OpenSSL::SSL::VERIFY_NONE # should use VERIFY_PEER in production
	request = Net::HTTP::Get.new(uri.request_uri)
	data= http.request(request).body
else
	data= Net::HTTP.get_response(URI.parse(label_url)).body
end
```
<br />
```
client = nil;

f_crt = File.read(SSL_CRT_PATH)
f_key = File.read(SSL_KEY_PATH)

api_url = "https://URL"

ssl_client_cert = OpenSSL::X509::Certificate.new(f_crt);
ssl_client_key = OpenSSL::PKey::RSA.new(f_key, SSL_KEY_PASSWORD);

client = RestClient::Resource.new(
	api_url,
	:ssl_client_cert => ssl_client_cert,
	:ssl_client_key => ssl_client_key,
	:verify_ssl => false
);

client.get()
```
