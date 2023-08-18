# **Navigate & Nested Routes**

Now we will focus on redirect. Delete all the query params from the route to post first.

## **Navigate**

Let's change a little bit our Post component. Import Navigate from react.

```jsx
// Post

import { Navigate, useNavigate } from 'react';

export default function Post() {
	const status = 404;

	const navigate = useNavigate();

	const handleClick = () => {
		console.log('Hello');
		navigate('/about');
	};

	if (status === 404) {
		return <Navigate to="/notfound" />;
	}

	return (
		<div>
			<h1>Post</h1>
			<button onClick={handleClick}>Click</button>
		</div>
	);
}
```

## **Nested Routes**

To create nested routes in the post file we can bring react router.

```jsx
// Post

import { Navigate, useNavigate, Routes, Rout } from 'react';

export default function Post() {
	const status = 404;

	const navigate = useNavigate();

	const handleClick = () => {
		console.log('Hello');
		navigate('/about');
	};

	if (status === 404) {
		return <Navigate to="/notfound" />;
	}

	return (
		<div>
			<h1>Post</h1>
			<button onClick={handleClick}>Click</button>
			<Routes>
				<Route path="/show" element={<h1>Hello World</h1>} />
			</Routes>
		</div>
	);
}
```

In order for nested routs to work we need to place \* after post path in App.js route.

After all we can delete all the code from last three section.
