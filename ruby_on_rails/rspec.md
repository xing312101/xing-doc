# RSpec
> references: http://rspec.info/

> https://relishapp.com/rspec

> https://github.com/rspec/rspec

> http://rspec.info/documentation/3.7/rspec-rails/


## install
```
1.
gem install rspec
or Gemfile
gem 'rspec'

2.
rspec --init

# can use rspec --help

3. run spec
vim project/spec/sandwich_spec.rb # write spec
rspec sandwich_spec.rb # do test
--------------
rspec --format documentation # rspec -fd
rspec --profile 2 # 看最慢的兩個測試
rspec -e milk -fd # running by name, 進行milk測試
rspec --only-failures
rspec --tag last_run_status:failed
```

## sample
```
# sample
Sandwich = Struct.new(:taste, :toppings)
def sandwich
	@sandwich ||= Sandwich.new('delicious', [])
end

RSpec.describe 'An ideal sandwich' do
	before {
		sandwich()
	}

	it 'is delicious' do
		taste = @sandwich.taste
		expect(taste).to eq('delicious')
	end
	it 'lets me add toppings' do
		@sandwich.toppings << 'cheese'
		toppings = @sandwich.toppings
		expect(toppings).not_to be_empty
	end
end

## result
fcontext 'with milk' do
same as
context 'with milk', focus: true do
```

## Syntax Highlighting
```
gem install coderay
gem install coderay -v 1.1.1
rspec -fd
```

## rspec --only-failures
```
RSpec.configure do |config|
	config.example_status_persistence_file_path = 'spec/examples.txt'
end
```

## rspec do focus on fcontext
```
# replace "context" to "fcontext" in spec file.

RSpec.configure do |config|
	config.filter_run_when_matching(focus: true)
	config.example_status_persistence_file_path = 'spec/examples.txt'
end
```

## Practice coffee_spec.rb
```
RSpec.configure do |config|
	config.filter_run_when_matching(focus: true)
	config.example_status_persistence_file_path = 'spec/examples.txt'
end

class Coffee
	def ingredients
		@ingredients ||= []
	end

	def add(ingredient)
		ingredients << ingredient
	end

	def price
		1.00
	end

	def color
		ingredients.include?(:milk) ? :light : :dark
	end

	def temperature
		ingredients.include?(:milk) ? 190.0 : 205.0
	end
end

RSpec.describe 'A cup of coffee' do
	let(:coffee) {Coffee.new}

	it 'costs $1' do
		expect(coffee.price).to eq(1.00)
	end

	context 'with milk' do
		before { coffee.add :milk }

		it 'is light in color' do
			pending 'Color not implemented yet'
			expect(coffee.color).to be(:light)
		end

		it 'is cooler than 200 degrees Fahrenheit' do
			pending 'Temperature not implemented yet'
			expect(coffee.temperature).to be < 200.0
		end


		it 'costs $1.25' do
			expect(coffee.price).to eq(1.25)
		end
	end
end
```

## Practice sandwich_spec.rb
```
Sandwich = Struct.new(:taste, :toppings)
def sandwich
	@sandwich ||= Sandwich.new('delicious', [])
end

RSpec.describe 'An ideal sandwich' do
	before {
		sandwich()
	}

	it 'is delicious' do
		taste = @sandwich.taste
		expect(taste).to eq('delicious')
	end
	it 'lets me add toppings' do
		@sandwich.toppings << 'cheese'
		toppings = @sandwich.toppings
		expect(toppings).not_to be_empty
	end
end
```

## Practice slow_spec.rb
```
RSpec.describe 'The sleep() method' do
	it('can sleep for 0.1 second') { sleep 0.1 }
	it('can sleep for 0.2 second') { sleep 0.2 }
	it('can sleep for 0.3 second') { sleep 0.3 }
	it('can sleep for 0.4 second') { sleep 0.4 }
	it('can sleep for 0.5 second') { sleep 0.5 }
end
```
