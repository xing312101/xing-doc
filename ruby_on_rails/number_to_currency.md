# number_to_currency
```
number_to_currency(1234567890.50) # => $1,234,567,890.50
number_to_currency(1234567890.506) # => $1,234,567,890.51
number_to_currency(1234567890.506, precision: 3) # => $1,234,567,890.506
number_to_currency(1234567890.506, locale: :fr) # => 1 234 567 890,51
number_to_currency("123a456") # => $123a456
number_to_currency("123a456", raise: true) # => InvalidNumberError
number_to_currency(-1234567890.50, negative_format: "(%u%n)") # => ($1,234,567,890.50)
number_to_currency(1234567890.50, unit: "£", separator: ",", delimiter: "") # => £1234567890,50
number_to_currency(1234567890.50, unit: "£", separator: ",", delimiter: "", format: "%n %u") # => 1234567890,50 £
```
