# **Form Input State**

In this section we will create form that will add new comments to our feedback array. Let's create FeedbackForm component and scaffold basic structure and bring it into App.js.

First thing to do is to bring Card component that form element will be wrapped in.

Our form will accept two kinds of input, text and radio button ratings. But now we will create text input.

For now we are going to create regular button element but in next section we will replace it with custom button component that will take in props.

```jsx
// FeedbackForm.jsx

import Card from './shared/Card';

export default function FeedbackForm() {
	return (
		<Card>
			<form>
				<h2>How would you rate your service with us</h2>
				<div className="input-group">
					<input type="text" placeholder="Write a review" />
					<button type="submit">Send</button>
				</div>
			</form>
		</Card>
	);
}
```

Typically when we have a form we want to have a piece of state for each input. Now let's create state for that text input we just created.

With state imported we can set the state by passing function to the event.

```jsx
// FeedbackForm.jsx

import { useState } from 'react';
import Card from './shared/Card';

export default function FeedbackForm() {
	const [text, setText] = useState('');

	const handleText Change = (e) => {
		setText(e.target.value);
	};

	return (
		<Card>
			<form>
				<h2>How would you rate your service with us?</h2>
				<div className="input-group">
					<input onChange={handleTextChange} type="text" placeholder="Write a review" value={text} />
					<button type="submit">Send</button>
				</div>
			</form>
		</Card>
	);
}
```
