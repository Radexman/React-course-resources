# **Conditionals**

Our React code can make decisions on specific conditions that we can set.

```jsx
// App.js
export default function App() {
	const loading = true;

	if (loading) return <h1>Loading...</h1>;

	return (
		<div>
			<h1>My App</h1>
			<p>Content has been loaded</p>
		</div>
	);
}
```

If the loading variable is set to true we will see returned markup. Common use case is when fetching data from backend, we want to inform user that something is going on in the background and display some kind of loading screen.

We can dynamically display any kind of content eg. comment section from previous module.

```jsx
// App.js

export default function App() {
	const comments = [
		{ id: 1, text: 'Post One' },
		{ id: 2, text: 'Post Two' },
		{ id: 3, text: 'Post Three' },
	];

    const showComments = false;

    return (
        <div className='comments'>
            {showComments ? (<h2>Comments ({comments.length})</div>
            <ul>
                {comments.map((comment, index) => (
                    <li key={index}>comment.text</li>
                ))}
            </ul>) : null}
        </div>
    )
}
```

To make a conditional statement we usually create a ternary operator expression.

We can also use the _&&_ operator to check if the property in the left is true and if it is, the cone on the right will be rendered.

```jsx
// App.js

export default function App() {
	const comments = [
		{ id: 1, text: 'Post One' },
		{ id: 2, text: 'Post Two' },
		{ id: 3, text: 'Post Three' },
	];

	const showComments = true;

	return (
		<div className="comments">
			{showComments && (
                <h2>Comments ({comments.length})</h2>
				<ul>
					{comments.map((comment, index) => (
						<li key={index}>{comment.text}</li>
					))}
				</ul>
			)}

		</div>
	);
}
```
