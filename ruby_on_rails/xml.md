# XML
> reference: https://ruby-doc.org/stdlib-2.2.3/libdoc/rexml/rdoc/REXML/Document.html

```
require "rexml/document"

file = File.new( "mydoc.xml" )
doc = REXML::Document.new file
status_code= doc .elements["Response/Status/Code"].text
doc.elements.each("*/section/item") { |element| puts element.attributes["upc"] }
```
