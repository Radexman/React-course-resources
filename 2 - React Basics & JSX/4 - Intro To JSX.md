# **Intro To JSX**

JSX allows us to write plain HTML in our components. There are a couple rules to follow when writing JSX.
React components are regular JavaScript functions, but their names must start with a capital letter or they won’t work!

```jsx
// App.js

function App() {
	return <h1>Hello from the App component</h1>;
}
```

Returning single HTML tag dos not require to wrap it in parentheses but multiple tags need to be wrapped.

```jsx
// App.js

function App() {
	return (
		<div>
			<h1>Hello from the App component</h1>
			<p>Hello World</p>
		</div>
	);
}
```

Writing multiple HTML tags without wrapping div will cause an error and they need to be wrappen in a container.

```jsx
// App.js

// This syntax will cause an error

function App() {
	return (
		<h1>Hello from the App component</h1>
        <p>Hello World</p>
	);
}
```

There is no need to write any specific wrapper tag, we can just leave empty angle brackets. This element is called the fragment.

```jsx
// App.js

function App() {
	return (
		<>
			<h1>Hello from the App component</h1>
			<p>Hello World</p>
		</>
	);
}
```

To add classes to our HTML markup we need to switch the _class_ keyword to _className_ because the _class_ syntax is reserved for JavaScript classes module.

```jsx
// App.js

// class tag will not work like in regular HTML

function App() {
	return (
		<div>
			<h1 class="text-xl">Hello from the App component</h1>
			<p>Hello World</p>
		</div>
	);
}
```

Use the className tag instead.

```jsx
// App.js

function App() {
	return (
		<div>
			<h1 className="text-xl">Hello from the App component</h1>
			<p>Hello World</p>
		</div>
	);
}
```

Another attribute we can't use in JSX is label for attribute because in JavaScript it is reserved for 'for' loops. We need to add htmlFor attribute.

```jsx
// App.js

function App() {
	return <label htmlFor="label">Form Input Label</label>;
}
```

We can get the same DOM elements without using JSX with just JavaScript.

```js
// App.js

import React from 'react';

function App() {
	return React.createElement('div', { className: 'container' }, React.createElement('h1', {}, 'My App'));
}
```

This is compleatly valid way of creating markup but regular JSX is much more human readable and it is advised to use JSX or TSX.
