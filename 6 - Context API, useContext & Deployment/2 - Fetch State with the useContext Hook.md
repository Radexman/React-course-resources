# **Fetch State with the useContext Hook**

Now that we created a context with the provider and some global state it's time to fetch it and get it to work.

Right now our FeedbackList is getting data from the global state not from context. Let's go to our FeedbackList component and change that.
We have to bring in useContext Hook and our context that we created.

Next all we have to do is to go into our component function and exteact needed data from our context using useContext Hook.

```jsx
// FeedbackList.jsx

...

import { useContext } from 'react';
import FeedbackContex from '../context/FeedbackContext';

export default function({ handleDelete }) {
    const {feedback} = useContext(FeedbackContext);

    ...
}

...
```

Now we can get rid of the prop we passed in because now we get the data from context and not from the props. Delete feedback desteuctured in the FeedbackList and passed props in that component in App.js file.

Now we will focus on refactoring our app from using state by props to getting it from the context.

Next component that uses feedback data is FeedbackStats, our component responsible for displaying data in the screen. We no longer need to destructure feedback from the function and also we can get rid of prop type.

```jsx
// FeedbackStats.jsx

import { useContext } from 'react';
import FeedbackContex from '../context/FeedbackContext';

export default function FeedbackStats() {
	const { feedback } = useContext(FeedbackContext);

    ...
}
```
