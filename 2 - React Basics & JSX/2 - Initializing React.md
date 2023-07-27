# **Initializing React**

Create a file in src folder called index.js, this is a entry point for webpack bundler. Under the hood React is bundling all the js files into one single bundle.js file using Webpack.

In the index.js first thing to do is to import React, React DOM and create root element for our application.Create in the src an index.css file and import it to index.js.

In src directory create App.js, this will be our main component.

```jsx
// index.js
import React from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';
import './index.css';
```

Next thing to do is to create our root element.

```jsx
// index.js
const container = document.getElementById('root');
const root = createRoot(container);
```

Then render it.

```jsx
// index.js
root.render(
	<React.StrictMode>
		<App />
	</React.StrictMode>
);
```

In the App.js we create a functional component called App and then we export it as a default

In React we write in **JSX** or **TSX** which are XML like syntax. JSX and TSX allow to write HTML directy into our JavaScript code.

```jsx
// App.js
function App() {
	return <h1>Hello from the App component</h1>;
}

export default App;
```
