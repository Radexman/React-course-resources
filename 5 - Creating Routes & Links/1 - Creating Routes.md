# **Creating Routes**

In React we don't have built in routung so we need to import it from the package called react-router-dom.

```npm
npm i react-router-dom
```

Let's creat a About Page compoenet that will be our /about page.

```jsx
// AboutPage.jsx
import Card from '../components/shared/Card';

export default function AboutPage() {
	return (
		<Card>
			<h1 className="about">About This Project</h1>
			<p>This is a React app to leave feedback for product or service</p>
			<p>Version: 1.0.0</p>

            <p>
                <a href='/'>Back To Home<a/>
            </p>
		</Card>
	);
}
```

We need to import React Router to App.js and wrap our app content in exact routes.

```jsx
// App.js
import { BrowserRoutes as Router, Route, Routes } from 'react-router-dom';
import Header from './components/Header';
import FeedbackList from './components/FeedbackList';
import FeedbackStats from './components/FeedbackState';
import FeedbackForm from './components/FeedbackForm';

export default function App() {
	return (
		<Router>
			<Header />
			<div className="container">
				<Routes>
					<Route
						exact
						path="/"
						element={
							<>
								<FeedbackForm handleAdd={addFeedback} />
								<FeedbackStats feedback={feedback} />
								<FeedbackList feedback={feedback} handleDelete={deleteFeedback} />
							</>
						}
					></Route>

					<Route path="/about" element={<AboutPage />} />
				</Routes>
			</div>
		</Router>
	);
}
```
