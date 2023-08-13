# **Add Feedback**

Now we can reate event that will pass in the feedback object to the App level state and render new comment.

```jsx
// FeedbackForm.jsx

fucntion FeedbackForm({ handleAdd })

const handleSubmit = (e) => {
    e.preventDefault();

    if(text.trim().length > 10) {
        const newFeedback = {
            text,
            rating
        }

        handleAdd(newFeedback);

        setText('');
    }
}

<form onSubmit={handleSubmit}>
```

```jsx
// App.js

const addFeedback = (newFeedback) => {
    setFeedback([newFeedback, ...feedback])
}

<FeedbackForm handleAdd={addFeedback}>
```

We need to install package for creating id.

```npm
npm i uuid
```

```jsx
// App.js

import { v4 as uuidv4 } from 'uuid';

const addFeedback = (newFeedback) => {
	newFeedback.id = uuidv4();
	setFeedback([newFeedback, ...feedback]);
};
```
