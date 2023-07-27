# **Dynamic Values & Lists in JSX**

Lists allow us to loop through data structures and output them dynamically on the page.

```jsx
// App.js

export default function App() {
	const title = 'Blog Post';
	const body = 'This is my blog';

	return (
		<div className="container">
			<h1>{title.toUpperCase()}</h1>
			<p>{body}</p>
		</div>
	);
}
```

Inside of the curly braces we can write any JavaScript expression.

```jsx
// App.js

export default function Calculation() {
	return (
		<div>
			<h1>Calculation result</h1>
			<h2>{Math.floor(Math.random) * (5 + 5)}</h2>
		</div>
	);
}
```

Creating list dynamically using _map_ high order array method,
and display number of items.

```jsx
// App.js

export default function App() {
	const comments = [
		{ id: 1, text: 'Post One' },
		{ id: 2, text: 'Post Two' },
		{ id: 3, text: 'Post Three' },
	];

	return (
		<div className="comments">
			<h3>Comments ({comments.length})</h3>
			<ul>
				{comments.map((comment, index) => (
					<li key={index}>{comment.text}</li>
				))}
			</ul>
		</div>
	);
}
```

When creating a list we need to add _key_ prop to the li, this value can be a index from the map method or original array. When fetching data from API _key_ prop can be an item id from the database.
