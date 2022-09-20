# Hash
```
to Object
	a = OpenStruct.new({:a=>1,:b=>2})
	a.a => 1
	a.b => 2
	用引號和冒號
	rgb = { black: '#000000', white: '#FFFFFF' }.with_indifferent_access
	rgb[:black] => "#000000"
	rgb['black'] => "#000000"

get keys array
	{:a=>1, :b=>2, :c=>3}.keys => [:a, :b, :c]

get values array
	{:a=>1, :b=>2, :c=>3}.values => [1, 2, 3]
合併
	hash = { :a => 'a' }
	# 不存回原hash
	hash.merge(:b => 'b')
	# => {:a=>'a',:b=>'b'}
	hash => { :a => 'a' }
	存回原hash
	hash.merge!(:b => 'b')
	# => {:a=>'a',:b=>'b'}
	hash => {:a=>'a',:b=>'b'}
```
