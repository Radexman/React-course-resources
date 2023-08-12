# **Custom Button Component**

Now we will create Button component that can be customized.

In our shared directory let's create Button component and set up bacic component structure.

We will need to destructure couple props.

-   children - This is wrapper component so we need this prop to be dyncmic.
-   version - Prop for different button styling.
-   type - Type of button action.
-   isDisabled - Boolean value for disabling and enabling button.

```jsx
// Button.jsx

export default function Button({ children, version, type, isDisabled }) {
	return (
		<button type={type} disabled={isDisabled} className={`btn btn-${version}`}>
			{children}
		</button>
	);
}
```

Okay so that's quite a customizavle component, last thing to do here is to set default props and prop types.

```jsx
// Button.jsx

import PropTypes from 'prop-types';

export default function Button({ children, version, type, isDisabled }) {
	return (
		<button type={type} disabled={isDisabled} className={`btn btn-${version}`}>
			{children}
		</button>
	);
}

Button.defaultProps = {
	version: 'primary',
	type: 'button',
	isDisabled: false,
};

Button.propTypes = {
	children: PropTypes.node.isRequired,
	version: PropTypes.string,
	type: PropTypes.string,
	isDisabled: PropTypes.bool,
};
```

Now that button component is created we can bring it in to our FeedbackForm component and pass in some props to customize it and adjust it to our needs.

```jsx
// FeedbackForm.jsx

import { useState } from 'react';
import Card from './shared/Card';
import Button from './shared/Button';

export default function FeedbackForm() {
	const [text, setText] = useState('');

	const handleTextChange = (e) => {
		setText(e.target.value);
	};

	return (
		<Card>
			<form>
				<h2>How would you rate your service with us?</h2>
				<div className="input-group">
					<input onChange={handleTextChange} type="text" placeholder="Write a review" value={text} />
					<Button type="submit" version="secondary" isDisabled={true}>
						Submit
					</Button>
				</div>
			</form>
		</Card>
	);
}
```
