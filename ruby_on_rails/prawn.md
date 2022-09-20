# prawn
> reference:

> https://github.com/prawnpdf/prawn

> http://prawnpdf.org/manual.pdf

製作pdf

## prawn image with base64
```
require 'prawn'
require 'tempfile'
require 'active_support' # for base64

Prawn::Document.generate('/tmp/test.pdf') do
	file = Tempfile.new('image')
	file.write ActiveSupport::Base64.decode64(image)
	file.close

	image file.path
end
```
