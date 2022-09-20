# Unorganized
# React
> reference: https://reactjs.org/

> tools: https://github.com/facebook/react-devtools

```
class ClassName extends React.Component {
	constructor(props) {
		super(props);
		this.handleSomething= this.handleSomething.bind(this);
		this.state = {attr: 'Attr'};
	}

	handleSomething() {
		this.setState({attr: 'aTTR'});
	}

	render() {
		return (
			<div>
			</div>
		);
	}
}

ReactDOM.render(
	<ClassName />,
	document.getElementById('root')
);
```

## Learning 快速瀏覽(需重新整理或重新coding)

### hello
```
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
	<h1>Hello, world!</h1>,
	document.getElementById('root')
);
```

### Introducing JSX
```
function formatName(user) {
	return user.firstName + ' ' + user.lastName;
}

const user = {
	firstName: 'Harper',
	lastName: 'Perez'
};

const element = (
	<h1>
	Hello, {formatName(user)}!
	</h1>
);

ReactDOM.render(
	element,
	document.getElementById('root')
);
```

### JSX Prevents Injection Attacks
```
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```

### create element
```
const element = React.createElement(
	'h1',
	{className: 'greeting'},
	'Hello, world!'
);

const element = {
	type: 'h1',
	props: {
	className: 'greeting',
	children: 'Hello, world'
	}
};
```

### rendering elements
```
<div id="root"></div>

const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### update element
```
function tick() {
	const element = (
		<div>
			<h1>Hello, world!</h1>
			<h2>It is {new Date().toLocaleTimeString()}.</h2>
		</div>
	);
	ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);


# see composiing Componets
function Clock(props) {
	return (
		<div>
			<h1>Hello, wwwww1</h1>
			<h2>It is {props.toLocaleTimeString()}.</h2>
			//new Date().toLocaleTimeString()
		</div>
	);
}
ReactDOM.render(
	<Clock date={new Date()} />,
	//<Clock />,
	document.getElementById('tttt2')
);
```

### Functional and Class Components
```
function Welcome(props) {
	return <h1>Hello, {props.name}</h1>;
}

# ES6 class
class Welcome extends React.Component {
	render() {
		return <h1>Hello, {this.props.name}</h1>;
	}
}
```

### Rendering a Component
```
function Welcome(props) {
	return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
	ReactDOM.render(
	element,
	document.getElementById('root')
);
```

### Composing Components
```
function Welcome(props) {
	return <h1>Hello, {props.name}</h1>;
}

function App() {
	return (
		<div>
			<Welcome name="Sara" />
			<Welcome name="Cahal" />
			<Welcome name="Edite" />
		</div>
	);
}

ReactDOM.render(
	<App />,
	document.getElementById('root')
);
```

### Converting a Function to a Class
```
class Clock extends React.Component {
	render() {
		return (
			<div>
				<h1>Hello, world!</h1>
				<h2>It is {this.props.date.toLocaleTimeString()}.</h2>
			</div>
		);
	}
}
```

### Adding Local State to a Class
```
class Clock extends React.Component {
	constructor(props) {
		super(props);
		this.state = {date: new Date()};
	}

	render() {
		return (
			<div>
				<h1>Hello, world!</h1>
				<h2>It is {this.state.date.toLocaleTimeString()}.</h2>
			</div>
		);
	}
}

ReactDOM.render(
	<Clock />,
	document.getElementById('root')
);
```

### Adding Lifecycle Methods to a Class
```
class Clock extends React.Component {
	constructor(props) {
		super(props);
		this.state = {date: new Date()};
	}

	componentDidMount() {
		this.timerID = setInterval(
			() => this.tick(),
			1000
		);
	}

	componentWillUnmount() {
		clearInterval(this.timerID);
	}

	tick() {
		this.setState({
			date: new Date()
		});
	}

	render() {
		return (
			<div>
				<h1>Hello, world!</h1>
				<h2>It is {this.state.date.toLocaleTimeString()}.</h2>
			</div>
		);
	}
}
```

### Using State Correctly
```
this.setState({comment: 'Hello'});

# when State Updates May Be Asynchronous
this.setState((prevState, props) => ({
	counter: prevState.counter + props.increment
}));

OR

this.setState(function(prevState, props) {
	return {
		counter: prevState.counter + props.increment
	};
});
```

### State Updates are Merged
```
constructor(props) {
	super(props);
		this.state = {
		posts: [],
		comments: []
	};
}

#independently with separate setState() calls:
componentDidMount() {
	fetchPosts().then(response => {
		this.setState({
			posts: response.posts
		});
	});

	fetchComments().then(response => {
		this.setState({
			comments: response.comments
		});
	});
}
```

### Handling Events
```
function ActionLink() {
	function handleClick(e) {
		e.preventDefault();
		console.log('The link was clicked.');
	}

	return (
		<a href="#" onClick={handleClick}>
			Click me
		</a>
	);
}
```

### Toggle ES6
```
class Toggle extends React.Component {
	constructor(props) {
		super(props);
		this.state = {isToggleOn: true};

		// This binding is necessary to make `this` work in the callback
		this.handleClick = this.handleClick.bind(this);
	}

	handleClick() {
		this.setState(prevState => ({
			isToggleOn: !prevState.isToggleOn
		}));
	}

	render() {
		return (
			<button onClick={this.handleClick}>
			{this.state.isToggleOn ? 'ON' : 'OFF'}
			</button>
		);
	}
}

ReactDOM.render(
	<Toggle />,
	document.getElementById('root')
);
```

### bind callbacks
```
1.
class LoggingButton extends React.Component {
	// This syntax ensures `this` is bound within handleClick.
	// Warning: this is *experimental* syntax.
	handleClick = () => {
		console.log('this is:', this);
	}

	render() {
		return (
			<button onClick={this.handleClick}>
				Click me
			</button>
		);
	}
}

2.
class LoggingButton extends React.Component {
	handleClick() {
		console.log('this is:', this);
	}

	render() {
		// This syntax ensures `this` is bound within handleClick
		return (
			<button onClick={(e) => this.handleClick(e)}>
				Click me
			</button>
		);
	}
}
```

### Passing Arguments to Event Handlers
```
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

### Conditional Rendering
```
function UserGreeting(props) {
	return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
	return <h1>Please sign up.</h1>;
}

function Greeting(props) {
	const isLoggedIn = props.isLoggedIn;
	if (isLoggedIn) {
		return <UserGreeting />;
	}
	return <GuestGreeting />;
}

function LoginButton(props) {
	return (
		<button onClick={props.onClick}>
			Login
		</button>
	);
}

function LogoutButton(props) {
	return (
		<button onClick={props.onClick}>
			Logout
		</button>
	);
}

class LoginControl extends React.Component {
	constructor(props) {
		super(props);
		this.handleLoginClick = this.handleLoginClick.bind(this);
		this.handleLogoutClick = this.handleLogoutClick.bind(this);
		this.state = {isLoggedIn: false};
	}

	handleLoginClick() {
		this.setState({isLoggedIn: true});
	}

	handleLogoutClick() {
		this.setState({isLoggedIn: false});
	}

	render() {
		const isLoggedIn = this.state.isLoggedIn;

		let button = null;
		if (isLoggedIn) {
			button = <LogoutButton onClick={this.handleLogoutClick} />;
		} else {
			button = <LoginButton onClick={this.handleLoginClick} />;
		}

		return (
			<div>
				<Greeting isLoggedIn={isLoggedIn} />
				{button}
			</div>
		);
	}
}

ReactDOM.render(
	<LoginControl />,
	document.getElementById('root')
);
```

### Inline If with Logical && Operator
```
function Mailbox(props) {
	const unreadMessages = props.unreadMessages;
	return (
		<div>
		<h1>Hello!</h1>
		{unreadMessages.length > 0 &&
			<h2>
				You have {unreadMessages.length} unread messages.
			</h2>
		}
		</div>
	);
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
	<Mailbox unreadMessages={messages} />,
	document.getElementById('root')
);
```

### Inline If-Else with Conditional Operator
```
render() {
	const isLoggedIn = this.state.isLoggedIn;
	return (
		<div>
		{isLoggedIn ? (
			<LogoutButton onClick={this.handleLogoutClick} />
		) : (
			<LoginButton onClick={this.handleLoginClick} />
		)}
		</div>
	);
}
```

### Lists and Keys
```
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
```

### Rendering Multiple Components
```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
	<li>{number}</li>
);

ReactDOM.render(
	<ul>{listItems}</ul>,
	document.getElementById('root')
);
```

### Basic List Component
```
function NumberList(props) {
	const numbers = props.numbers;
	const listItems = numbers.map((number) =>
		<li key={number.toString()}>
			{number}
		</li>
	);
	return (
		<ul>{listItems}</ul>
	);
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
	<NumberList numbers={numbers} />,
	document.getElementById('root')
);
```

### keys
```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
	<li key={number.toString()}>
		{number}
	</li>
);

const todoItems = todos.map((todo) =>
	<li key={todo.id}>
		{todo.text}
	</li>
);

const todoItems = todos.map((todo, index) =>
	// Only do this if items have no stable IDs
	<li key={index}>
		{todo.text}
	</li>
);
```

### Extracting Components with Keys
```
function ListItem(props) {
	// Correct! There is no need to specify the key here:
	return <li>{props.value}</li>;
}

function NumberList(props) {
	const numbers = props.numbers;
	const listItems = numbers.map((number) =>
		// Correct! Key should be specified inside the array.
		<ListItem key={number.toString()}
			value={number} />

	);
	return (
		<ul>
			{listItems}
		</ul>
	);
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
	<NumberList numbers={numbers} />,
	document.getElementById('root')
);
```

### Keys Must Only Be Unique Among Siblings
```
#We can use the same keys when we produce two different arrays:
function Blog(props) {
	const sidebar = (
		<ul>
			{props.posts.map((post) =>
				<li key={post.id}>
					{post.title}
				</li>
			)}
		</ul>
	);
	const content = props.posts.map((post) =>
		<div key={post.id}>
			<h3>{post.title}</h3>
			<p>{post.content}</p>
		</div>
	);
	return (
		<div>
			{sidebar}
			<hr />
			{content}
		</div>
	);
}

const posts = [
	{id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
	{id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
	<Blog posts={posts} />,
	document.getElementById('root')
);
```

### Embedding map() in JSX
```
function NumberList(props) {
	const numbers = props.numbers;
	return (
		<ul>
			{numbers.map((number) =>
				<ListItem key={number.toString()}
				value={number} />

			)}
		</ul>
	);
}
```


## 純html用react
> references:
https://medium.com/@to_pe/how-to-add-react-to-a-simple-html-file-a11511c0235f

> https://babeljs.io/

```
<div id="root"></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.4.2/react.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.4.2/react-dom.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.21.1/babel.min.js"></script>
<script type="text/babel">
	class Greeting extends React.Component {
		render() {
			return (<p>Hello world</p>);
		}
	}
	ReactDOM.render(
		<Greeting />,
		document.getElementById('root')
	);
</script>
```

## Forms (需要重新整理)
> reference: https://reactjs.org/docs/forms.html

### Controlled Components
```
<form>
	<label>
		Name:
		<input type="text" name="name" />
	</label>
	<input type="submit" value="Submit" />
</form>

class NameForm extends React.Component {
	constructor(props) {
		super(props);
		this.state = {value: ''};

		this.handleChange = this.handleChange.bind(this);
		this.handleSubmit = this.handleSubmit.bind(this);
	}

	handleChange(event) {
		this.setState({value: event.target.value});
	}

	handleSubmit(event) {
		alert('A name was submitted: ' + this.state.value);
		event.preventDefault();
	}

	render() {
		return (
		<form onSubmit={this.handleSubmit}>
			<label>
				Name:
				<input type="text" value={this.state.value} onChange={this.handleChange} />
			</label>
			<input type="submit" value="Submit" />
		</form>
		);
	}
}
```

### The textarea Tag
```
class EssayForm extends React.Component {
	constructor(props) {
		super(props);
		this.state = {
			value: 'Please write an essay about your favorite DOM element.'
		};

		this.handleChange = this.handleChange.bind(this);
		this.handleSubmit = this.handleSubmit.bind(this);
	}

	handleChange(event) {
		this.setState({value: event.target.value});
	}

	handleSubmit(event) {
		alert('An essay was submitted: ' + this.state.value);
		event.preventDefault();
	}

	render() {
		return (
			<form onSubmit={this.handleSubmit}>
				<label>
					Essay:
					<textarea value={this.state.value} onChange={this.handleChange} />
				</label>
				<input type="submit" value="Submit" />
			</form>
		);
	}
}
```

### The select Tag
```
class FlavorForm extends React.Component {
	constructor(props) {
		super(props);
		this.state = {value: 'coconut'};

		this.handleChange = this.handleChange.bind(this);
		this.handleSubmit = this.handleSubmit.bind(this);
	}

	handleChange(event) {
		this.setState({value: event.target.value});
	}

	handleSubmit(event) {
		alert('Your favorite flavor is: ' + this.state.value);
		event.preventDefault();
	}

	render() {
		return (
			<form onSubmit={this.handleSubmit}>
				<label>
					Pick your favorite La Croix flavor:
					<select value={this.state.value} onChange={this.handleChange}>
						<option value="grapefruit">Grapefruit</option>
						<option value="lime">Lime</option>
						<option value="coconut">Coconut</option>
						<option value="mango">Mango</option>
					</select>
				</label>
				<input type="submit" value="Submit" />
			</form>
		);
	}
}
```
#### Note:
You can pass an array into the value attribute, allowing you to select multiple options in a select tag:
```
<select multiple={true} value={['B', 'C']}>
```

### The file input Tag
> https://reactjs.org/docs/uncontrolled-components.html#the-file-input-tag

In React, an  is always an uncontrolled component because its value can only be set by a user, and not programmatically.
```
class FileInput extends React.Component {
	constructor(props) {
		super(props);
		this.handleSubmit = this.handleSubmit.bind(this);
	}
	handleSubmit(event) {
		event.preventDefault();
		alert(
			`Selected file - ${this.fileInput.files[0].name}`
		);
	}

	render() {
		return (
			<form onSubmit={this.handleSubmit}>
				<label>
					Upload file:
					<input
					type="file"
					ref={input => {
						this.fileInput = input;
					}}
					/>
				</label>
				<br />
				<button type="submit">Submit</button>
			</form>
		);
	}
}

ReactDOM.render(
	<FileInput />,
	document.getElementById('root')
);
```

### Handling Multiple Inputs
```
class Reservation extends React.Component {
	constructor(props) {
		super(props);
		this.state = {
			isGoing: true,
			numberOfGuests: 2
		};

		this.handleInputChange = this.handleInputChange.bind(this);
	}

	handleInputChange(event) {
		const target = event.target;
		const value = target.type === 'checkbox' ? target.checked : target.value;
		const name = target.name;

		this.setState({
			[name]: value
		});
	}

	render() {
		return (
			<form>
				<label>
					Is going:
					<input
					name="isGoing"
					type="checkbox"
					checked={this.state.isGoing}
					onChange={this.handleInputChange} />
				</label>
					<br />
				<label>
					Number of guests:
					<input
					name="numberOfGuests"
					type="number"
					value={this.state.numberOfGuests}
					onChange={this.handleInputChange} />
				</label>
			</form>
		);
	}
}
```
### Controlled Input Null Value

```
ReactDOM.render(<input value="hi" />, mountNode);

setTimeout(function() {
	ReactDOM.render(<input value={null} />, mountNode);
}, 1000);
```

## Composition
> https://reactjs.org/docs/composition-vs-inheritance.html

### props.children
```
function FancyBorder(props) {
	return (
		<div className={'FancyBorder FancyBorder-' + props.color}>
			{props.children}
		</div>
	);
}

function WelcomeDialog() {
	return (
		<FancyBorder color="blue">
			<h1 className="Dialog-title">
				Welcome
			</h1>
			<p className="Dialog-message">
				Thank you for visiting our spacecraft!
			</p>
		</FancyBorder>
	);
}
```
```
function SplitPane(props) {
	return (
		<div className="SplitPane">
			<div className="SplitPane-left">
				{props.left}
			</div>
			<div className="SplitPane-right">
				{props.right}
			</div>
		</div>
	);
}

function App() {
	return (
		<SplitPane
			left={
				<Contacts />
			}
			right={
				<Chat />
		} />
	);
}
```

### Specialization
```
function Dialog(props) {
	return (
		<FancyBorder color="blue">
			<h1 className="Dialog-title">
				{props.title}
			</h1>
			<p className="Dialog-message">
				{props.message}
			</p>
			{props.children}
		</FancyBorder>
	);
}

class SignUpDialog extends React.Component {
	constructor(props) {
		super(props);
		this.handleChange = this.handleChange.bind(this);
		this.handleSignUp = this.handleSignUp.bind(this);
		this.state = {login: ''};
	}

	render() {
		return (
			<Dialog title="Mars Exploration Program"
				message="How should we refer to you?">
				<input value={this.state.login}
				onChange={this.handleChange} />

				<button onClick={this.handleSignUp}>
					Sign Me Up!
				</button>
			</Dialog>
		);
	}

	handleChange(e) {
		this.setState({login: e.target.value});
	}

	handleSignUp() {
		alert(`Welcome aboard, ${this.state.login}!`);
	}
}
```

## Lifting State Up
> https://reactjs.org/docs/lifting-state-up.html

```
function BoilingVerdict(props) {
	if (props.celsius >= 100) {
		return <p>The water would boil.</p>;
	}
	return <p>The water would not boil.</p>;
}

class Calculator extends React.Component {
	constructor(props) {
		super(props);
		this.handleChange = this.handleChange.bind(this);
		this.state = {temperature: ''};
	}

	handleChange(e) {
		this.setState({temperature: e.target.value});
	}

	render() {
		const temperature = this.state.temperature;
		return (
			<fieldset>
				<legend>Enter temperature in Celsius:</legend>
				<input
					value={temperature}
					onChange={this.handleChange} />

				<BoilingVerdict
					celsius={parseFloat(temperature)} />

			</fieldset>
		);
	}
}
```

### Adding a Second Input
```
const scaleNames = {
	c: 'Celsius',
	f: 'Fahrenheit'
};

class TemperatureInput extends React.Component {
	constructor(props) {
		super(props);
		this.handleChange = this.handleChange.bind(this);
		this.state = {temperature: ''};
	}

	handleChange(e) {
		this.setState({temperature: e.target.value});
	}

	render() {
		const temperature = this.state.temperature;
		const scale = this.props.scale;
		return (
			<fieldset>
				<legend>Enter temperature in {scaleNames[scale]}:</legend>
				<input value={temperature}
				onChange={this.handleChange} />
			</fieldset>
		);
	}
}

class Calculator extends React.Component {
	render() {
		return (
			<div>
				<TemperatureInput scale="c" />
				<TemperatureInput scale="f" />
			</div>
		);
	}
}
```

### Writing Conversion Functions
```
function toCelsius(fahrenheit) {
	return (fahrenheit - 32) * 5 / 9;
}

function toFahrenheit(celsius) {
	return (celsius * 9 / 5) + 32;
}

function tryConvert(temperature, convert) {
	const input = parseFloat(temperature);
		if (Number.isNaN(input)) {
		return '';
	}
	const output = convert(input);
	const rounded = Math.round(output * 1000) / 1000;
	return rounded.toString();
}
```

### Lifting State Up complete
```
function toCelsius(fahrenheit) {
	return (fahrenheit - 32) * 5 / 9;
}

function toFahrenheit(celsius) {
	return (celsius * 9 / 5) + 32;
}

function tryConvert(temperature, convert) {
	const input = parseFloat(temperature);
	if (Number.isNaN(input)) {
		return '';
	}
	const output = convert(input);
	const rounded = Math.round(output * 1000) / 1000;
	return rounded.toString();
}

const scaleNames = {
	c: 'Celsius',
	f: 'Fahrenheit'
};

class TemperatureInput extends React.Component {
	constructor(props) {
		super(props);
		this.handleChange = this.handleChange.bind(this);
	}

	handleChange(e) {
		this.props.onTemperatureChange(e.target.value);
	}

	render() {
		const temperature = this.props.temperature;
		const scale = this.props.scale;
		return (
			<fieldset>
				<legend>Enter temperature in {scaleNames[scale]}:</legend>
				<input value={temperature}
					onChange={this.handleChange} />
			</fieldset>
		);
	}
}

class Calculator extends React.Component {
	constructor(props) {
		super(props);
		this.handleCelsiusChange = this.handleCelsiusChange.bind(this);
		this.handleFahrenheitChange = this.handleFahrenheitChange.bind(this);
		this.state = {temperature: '', scale: 'c'};
	}

	handleCelsiusChange(temperature) {
		this.setState({scale: 'c', temperature});
	}

	handleFahrenheitChange(temperature) {
		this.setState({scale: 'f', temperature});
	}

	render() {
		const scale = this.state.scale;
		const temperature = this.state.temperature;
		const celsius = scale === 'f' ? tryConvert(temperature, toCelsius) : temperature;
		const fahrenheit = scale === 'c' ? tryConvert(temperature, toFahrenheit) : temperature;

		return (
			<div>
			<TemperatureInput
				scale="c"
				temperature={celsius}
				onTemperatureChange={this.handleCelsiusChange} />

			<TemperatureInput
				scale="f"
				temperature={fahrenheit}
				onTemperatureChange={this.handleFahrenheitChange} />

			<BoilingVerdict
				celsius={parseFloat(celsius)} />

			</div>
		);
	}
}
```


