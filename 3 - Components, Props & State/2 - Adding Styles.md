# **Adding Styles**

There are a couple of ways of adding CSS styles into our components. We can import global style sheet or have separete css for each compontnt and then we simply we just import it. I prefer to use Tailwind CSS with inline classes.

We can apply out styles conditionally as props into JSX and even use default props with CSS rules.

Adding style directly into component style attribute. We need to put double curly braces because we are passing in an object.

```jsx
// Header.jsx

function Header({ text }) {
	return (
		<header
			style={{
				backgroundColor: 'blue',
				color: 'red',
			}}
		>
			<div className="container">
				<h2>{text}</h2>
			</div>
		</header>
	);
}
```

We can also put out styles into variable as an object.

```jsx
// Header.jsx

function Header({ text }) {
	const headerStyles = {
		backgroundColor: 'blue',
		color: 'red',
	};

	return (
		<header style={headerStyles}>
			<div className="container">
				<h2>{text}</h2>
			</div>
		</header>
	);
}
```

We can pass in props with styles

```jsx
// App.js

function App() {
	return (
		<>
			<Header bgColor="red" textColor="blue" />
			<div className="container">
				<h1>My App</h1>
			</div>
		</>
	);
}
```

And destructure them directly in the component

```jsx
// Header.jsx

function Header({ text, bgColor, textColor }) {
	const headerStyles = {
		backgroundColor: bgColor,
		color: textColor,
	};

	return (
		<header style={headerStyles}>
			<div className="container">
				<h2>{text}</h2>
			</div>
		</header>
	);
}
```

We can also set some default props purely for styling. If nothing is explicitly passen in the Header, default props will be applied.

```jsx
// Header.jsx

Header.defaultProps = {
	text: 'Feedback UI',
	bgColor: 'rgba(0,0,0,0.4)',
	textColor: '#ff6a95',
};
```

We can add these default props to our prop types as well.

```jsx
// Header.jsx

Header.propTypes = {
	text: PropTypes.string,
	bgColor: PropTypes.string,
	textColor: PropTypes.string,
};
```

There are multiple ways of doing styles in React. We can even use libraries like Styled Components that supply for us ready to use components. Other options are Shocker UI and Material UI.
