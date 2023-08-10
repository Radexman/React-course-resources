# **FeedbackStats Component**

Now we will implement dynamic stats tracking for more dynamic and robutst user experience. We will create Stats Component which will display amount of feedback and will display average rating. Let's start by creating FeedbackStats.jsx in components directory.

```jsx
// FeedbackStats.jsx

export default function FeedbackStats() {
    return ()
}
```

Bring that component into App.js and embed it in the container div. Than still in the App file we need to pass our global feedback state because we will need it to work with all the data that we want to dynamically display in FeedbackStats Component.

```jsx
// App.js

import { useState } from 'react';
import Header from './components/Header';
import FeedbackList from './components/FeedbackList';
import FeedbackData from './data/FeedbackData';
import FeedbackStats from './components/FeedbackStats';

export default function App() {
	const [feedback, setFeedback] = useState(FeedbackData);

	const deleteFeedback = (id) => {
		if (window.confirm('Are you sure you want to delete')) {
			setFeedback(feedback.filter((item) => item.id !== id));
		}
	};

	return (
		<>
			<Header />
			<div className="container">
				<FeedbackStats feedback={feedback} />
				<FeedbackList feedback={feedback} handleDelete={deleteFeedback} />
			</div>
		</>
	);
}
```

Here whenever feedback state changes the changes will be executed in the dependant components.

Now let's work on the actual FeedbackStats Component. We need to capture the event and display average ratuings and comments amount.

Getting array length is pretty simple

```jsx
// FeedbackStats.jsx

export default function FeedbackStats({ feedback }) {
	return (
		<div className="feedback-stats">
			<h4>{feedback.length}</h4>
			<h4></h4>
		</div>
	);
}
```

Next we need to calculate average ratings, reduce high order array mathod may come in handy here.

Let's also get rid of too many decimals after comma.

We will need to check if the average is NaN and make sure to display 0 if it is.

```jsx
// FeedbackStats.jsx

export default function FeedbackStats({ feedback }) {
	// Calculate average rating
	let average =
		feedback.reduce((acc, cur) => {
			return acc + cur.rating;
		}, 0) / feedback.length;

	average = average.toFixed(1).replace(/[.,]0$/, '');

	return (
		<div className="feedback-stats">
			<h4>{feedback.length}</h4>
			<h4>Average Rating: {isNaN(average) ? 0 : average}</h4>
		</div>
	);
}
```

Lastly let's add PropTypes.

```jsx
// FeedbackStats.jsx

import PropTypes from 'prop-types';

...

FeedbackStats.propTypes = {
	feedback: PropTypes.array.isRequired,
};
```
