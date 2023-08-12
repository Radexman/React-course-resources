# **Real-Time Validation**

In this section we will add some real time validation, the button will be disabled if the text input is empty or if the message will be shorter than 10 characters. We will achieve that by setting additional pieces of state. You can think of state as it is a dynamic value passed into the let variable.

```jsx
// FeedbackForm.jsx

import { useState } from 'react';
import Card from './shared/Card';
import Button from './shared/Button';

export default function FeedbackForm() {
	const [text, setText] = useState('');
	const [btnDisabled, setBtnDisabled] = useState(true);
	const [message, setMessage] = useState('');

	const handleTextChange = (e) => {
		if (text === '') {
			setBtnDisabled(true);
			setMessage(null);
		} else if (text !== '' && text.trim().length <= 10) {
			setBtnDisabled(true);
			setMessage('Review has to be at least 10 characters long');
		} else {
			setBtnDisabled(false);
			setMessage(null);
		}

		setText(e.target.value);
	};

	return (
		<Card>
			<form>
				<h2>How would you rate your service with us?</h2>
				<div className="input-group">
					<input onChange={handleTextChange} type="text" value={text} />
					<Button type="submit" version="secondary" isDisabled={btnDisabled}>
						Submit
					</Button>
				</div>
				{message && <div className="message">{message}</div>}
			</form>
		</Card>
	);
}
```
