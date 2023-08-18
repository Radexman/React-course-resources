# **Moving the Functions to the Context**

Now we will move the rest of our state into context.
Cut the delete feedback function from the App.js and put it into FeedbackContxt.js.

We will want to pass the deleteFeedback function into FeedbackProvider value.

```jsx
// FeedbackContext.js

import { createContext, useState } from 'react';

const FeedbackContext = createContext();

export const FeedbackProvider = ({ children }) => {
	const [feedback, setFeedback] = useState([
		{
			id: 1,
			text: 'This item is from context',
			rating: 10,
		},
	]);

    const deleteFeedback = (id) => {
        if(window.confirm('Are you sure you want to delete?)) {
            setFeedback(feedback.filter((item) => item.id !== id))
        }
    }

	return (
		<FeedbackContext.Provider
			value={{
				feedback,
                deleteFeedback
			}}
		>
			{children}
		</FeedbackContext.Provider>
	);
};
```

Now we can remove handleDelete prop from FeedbackList in App.js and delete handleDelete cathed directly in FeedbackList component.

Next let's go into our FeedbackItem and remove destructured handleDelete. We basically removed all the prop drilling from out application.

Still inside FeedbackItem we need to bring our useContext, FeedbackContext and get from it deleteFeedback function and replate handleDelete with it.

We can also get rid of prop types entirely from this file.

```jsx
// FeedbackItem

import { FaTimes as Xmark } from 'react-icons/fa';
import Card from './shared/Card';
import { useContext } from 'react';
import FeedbackContext from '../context/FeedbackContext';

export default function FeedbackItem({ item }) {
	const { deleteFeedback } = useContext(FeedbackContext);

	return (
		<Card>
			<div className="num-display">{item.rating}</div>
			<button onClick={() => deleteFeedback(item.id)}>
				<Xmark color="purple" />
			</button>
			<div className="text-display">{item.text}</div>
		</Card>
	);
}
```

Now that delete is replaced we need to take care of addFeedback function. Cut the addFeecback from the App.js
and bring it in to our context.

```jsx
// FeedbackContext.js
import { v4 as uuid4 } from 'uuid';
import { createContext, useState } from 'react';

const FeedbackContext = createContext();

export const FeedbackProvider = ({ children }) => {
	const [feedback, setFeedback] = useState([
		{
			id: 1,
			text: 'This item is from context',
			rating: 10,
		},
	]);

	const deleteFeedback = (id) => {
		if (window.confirm('Are you sure you want to delete?')) {
			setFeedback(feedback.filter((item) => item.id !== id));
		}
	};

	const addFeedback = (id) => {
		newFeedback.id === uuid4();
		setFeedback([newFeedback, ...feedback]);
	};

	return (
		<FeedbackContext.Provider
			value={{
				feedback,
				deleteFeedback,
				addFeedback,
			}}
		>
			{children}
		</FeedbackContext.Provider>
	);
};
```

We will need to remove uuid from the App.js and bring it into context file. At last we can add our function to the provider value.

Now we don't need to have state in App.js so let's get rid of it.

Inside FeedbackForm get rid of handleAdd and import useContext and get addFeedback from that context.

```jsx
// FeedbackForm.jsx
import { useContext } from 'react';
import FeedbackContex from '../context/FeedbackContext';

...

export default function FeedbackForm() {
    ...

    const {addFeedback} = useContext(FeedbackContext);

    ...
}

```

Now we have cleared our App.js file of the state and state setters. This is more clear and readable way of creating global state, especially when we have more of it, it can became very cluttered.
