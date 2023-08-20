## **Spinner Component**

Now we will create that spinner component I mendioned in the last section. We will need a spinner gif or an animated svg. Let's start by creating assets directry where we will store our gif and from where we will get the path to it.

Now we want this gif to show in the feedback list conditionally if the isLoading state is true and display the data if isLoading is false, so simple conditional rendering with the ternart operator.

```jsx
// FeedbackList.jsx

import { motion, AnimatePresence } from 'framer-motion';
import { useContext } from 'react';
import FeedbackItem from './FeedbackItem';
import FeedbackContext from '../context/FeedbackContext';

export default function FeedbackLis() {
	const { feedback, isLoading } = useContext(FeedbackContext);

	if (!isLoading && (!feedback || feedback.length === 0)) {
		return <p>No Feedback Yet</p>;
	}

	return isLoading ? (
		<Spinner />
	) : (
		<div className="feedback-list">
			<AnimatePresence>
				{feedback.map((item) => (
					<motion.div key={item.id} initial={{ opacity: 0 }} animate={{ opacity: 1 }} exit={{ opacity: 0 }}>
						<FeedbackItem key={item.id} item={item} />
					</motion.div>
				))}
			</AnimatePresence>
		</div>
	);
}
```

Okay so now that we have the logic for this conditional render it's time to create Spinner component. We will wrap the spinner gif in the Card component for styling pourpouses.

```jsx
// Spinner.jsx

import spinner from './assets/spinner.gif';
import Card from './Card';

export default function Spinner() {
	return (
		<Card>
			<img src={spinner} alt="Loading screen" style={{ width: '100px', margin: 'auto', display: 'block' }} />
		</Card>
	);
}
```
