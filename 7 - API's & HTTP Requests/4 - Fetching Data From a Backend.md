# **Fetching Data From a Backend**

So now that we created a mock backend we can finally display our data on the client side, let's refactor the code! Go to our context file and replace the feedback state with an empty array.

The next thing to do is to imporn useEffect hook because we will want our feedback to load while the page loads.

Let's call useEffect under the state declarations and call inside fetchFeedback function that we will create in a moment, leave the array inside this hook empty.

Now we will create an async function that will fetch while feedback data with some additional query params and it will update the state via setFeedback function.

Another important thing that we will start in this section is some kind of visual cue for the user that something is going on in the back, we will display a spinner when the data is fetched. But for now we will create a piece of state for that spinner which will take a boolean value and after data fetching is done will take in false value.

```jsx
// FeedbackContext.jsx

import { v4 as uuid4 } from 'uuid';
import { createContext, useState, useEffect } from 'react';

const FeedbackContext = createContext();

export const FeedbackProvider = ({ children }) => {
	const [isLoading, setIsLoading] = useState(true);
	const [feedback, setFeedback] = useState([]);
	const [feedbackEdit, setFeedbackEdit] = useState({
		item: {},
		idEdit: false,
	});

	useEffect(() => {
		fetchFeedback();
	}, []);

	// Fetch feedback
	const fetchFeedback = async () => {
		const res = await fetch('http://localhost:5000/feedback?_sort=id&_order=desc');
		const data = await res.json();

		setFeedback(data);
		setIsLoading(false);
	};

	const editFeedback = (item) => {
		setFeedbackEdit({
			item,
			isEdit: true,
		});
	};

	const updateFeedback = (id, updItem) => {
		setFeedback(feedback.map((item) => (item.id === id ? { ...item, ...updItem } : item)));
	};

	const deleteFeedback = (id) => {
		if (window.confirm('Are you sure you want to delete?')) {
			setFeedback(feedback.filter((item) => item.id !== id));
		}
	};

	const addFeedback = (newFeedback) => {
		newFeedback.id = uuid4();
		setFeedback([newFeedback, ...feedback]);
	};

	return (
		<FeedbackContext.Provider
			value={{
				feedback,
				feedbackEdit,
				isLoading,
				deleteFeedback,
				addFeedback,
				editFeedback,
				updateFeedback,
			}}
		>
			{children}
		</FeedbackContext.Provider>
	);
};
```
