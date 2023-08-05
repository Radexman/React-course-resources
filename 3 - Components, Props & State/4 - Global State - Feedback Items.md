# **Global State - Feedback Items**

In our App.js we will create global level state that will be passed down to other components.

Let's start with the import of useState and set feedback state at app level component. Let's also create separate data file with FeedbackData.js and import it and pass as default state.

```jsx
// App.js

import { useState } from 'react';
import Header from './components/Header';
import FeedbackData from './data/FeedbackData';

export default function App() {
	const [feedback, setFeedback] = useState(FeedbackData);

	return (
		<>
			<Header />
			<div className="container"></div>
		</>
	);
}
```

Our FeedbackData file should include array of objects formatted this way:

```js
// FeedbackData.js

const feedback = [
	{
		id: 1,
		rating: 10,
		text: 'Example Feeback One',
	},
	{
		id: 2,
		rating: 9,
		text: 'Example Feeback Two',
	},
	{
		id: 3,
		rating: 8,
		text: 'Example Feeback Three',
	},
];

export default feedback;
```

Structure of this JS file resambles JSON structure often used to talk with app's API. This kind of dynamic data is often fetched from the server. We should see this array in dev tools state.

Next we need to create FeedbackList in which our Feedback Items will be created. Import FeedbackList and delete FeedbackItem from the App.js component. Also change embedded FeedbackItem component to FeedbackList component. Pass in this component feedback prop.

```jsx
// App.js

import { useState } from 'react';
import Header from './components/Header';
import FeedbackList from './components/FeedbackList';
import FeedbackData from './data/FeedbackData';

export default function App() {
	const [feedback, setFeedback] = setState(feedback);

	return (
		<>
			<Header />
			<div className="container">
				<FeedbackList feedback={feedback} />
			</div>
		</>
	);
}
```

Next follow with this code

```jsx
// FeedbackList.jsx

import FeedbackItem from './Feedbacktem';

export default function FeedbackList({ feedback }) {
	if (!feedback || feedback.length === 0) {
		return <p>No Feedback Yet</p>;
	}

	return (
		<div className="feedback-list">
			{feedback.map((item) => (
				<FeedbackItem key={item.id} item={item} />
			))}
		</div>
	);
}
```

In the code above we destructured feedback prop passed from the app level sate and checked if the feedback even exists. It is a good practice to handle these kind of cases and return conditially propper information.

Next we need to use higher order array method called map to render our feedback items. Open new JSX expression curly baraces and map through feedback array.

Create FeedbackItem component and pass in a key prop that is used to destinguish between items and pass in the item prop to destructure information from it directly in the FeedbcakItem component.

Next thing is to delete all states from the FeedbackItem component and destructure prop passed in the FeddbackList component.

```jsx
export default function FeedbackItem({ item }) {
	return (
		<div className="card">
			<div className="num-display">{item.rating}</div>
			<div className="text-displat">{item.text}</div>
		</div>
	);
}
```

Pass in propperties in JSX expressions inside divs.

In this way we can display dynamic data with app level state and by mapping through arrays of data. For each item is createt separate div that makes our code more DRY and more React.
