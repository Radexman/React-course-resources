# **Update Feedback Item**

So now we can finally create the functionality to update that feedback item. In the previous sections we created new pieces of state and focused in edit mode.

Let's create in our context function for updating feedback.
Our updateFeedback function needs to be accesed in the form so we need to pass it into FeedbackContext Provider value param.

```jsx
// FeedbackContext.js

import { createContext, useState } from 'react';
import { v4 as uuid4 } from 'uuid';

const FeedbackContext = createContext();

export const FeedbackProvider = ({ children }) => {
    const [feedback, setFeedback] = useState([
        {
            id: 1,
            text: 'This is feedback item One',
            rating: 10
        }
        {
            id: 2,
            text: 'This is feedback item Two',
            rating: 9
        }
        {
            id: 3,
            text: 'This is feedback item Three',
            rating: 7
        }
    ]);

    // Update feedback item
    const updateFeedback = (id, updItem) => {
        setFeedback(feedback.map((item) => item.id === id) ? { ...item, ...updItem } : item);
    }

    // Set item to be updated
    const editFeedback = (item) => {
        setFeedbackEdit({
            item,
            isEdit: true
        })
    }

    // Delete selected item
    const deleteFeedback = (id) => {
        if(window.confirm('Are you sure you want to delete?')) {
            setFeedback(feedback.filter(item) => item.id !== id)
        }
    }

    // Add new feedback item
    const addFeedback = (newFeedback) => {
        newFeedback.id = uuid4();
        setFeedback([newFeedback, ...feedback]);
    }

    return (
        <FeedbackContext.Provider value={{
            feedback,
            deleteFeedback,
            addFeedback,
            editFeedback,
            feedbackEdit,
            updateFeedback
        }}>
            {children}
        </FeedbackContext.Provider>
    )
}

export default FeedbackContext;
```

In the form now we need to get that function from the context. We will want to call that function in the handleSubmit function but let's first add a checker to see if the item is in the edit mode or not.

```jsx
// FeedbackForm.jsx

import { useState, useContext, useEffect } from 'react';
import Card from './shared/Card';
import Button from './shared/Button';
import RatingSelect from './RatingSelect';
import FeedbackContext from '../context/FeedbackContext';

export default function FeedbackForm() {
	const [text, setText] = useState('');
	const [rating, setRating] = useState();
	const [btnDisabled, setBtnDisabled] = useState(true);
	const [message, setMessage] = useState('');

	const { addFeedback, feedbackEdit, updateFeedback } = useContext(FeedbackContext);

	useEffect(() => {
		if (feedbackEdit.edit === true) {
			setBtnDisabled();
			setText(feedbackEdit.item.text);
			setRating(feedbackEdit.item.rating);
		}
	}, [feedbackEdit]);

	const handleTextChange = (e) => {
		if (text === '') {
			setBtnDisabled(true);
			setMessage(null);
		} else if (text !== '' && text.trim().length <= 10) {
			setBtnDisabled(true);
			setMessage('Comment has to be at least 10 characters long');
		} else {
			setMessage('');
			setBtnDisabled(false);
		}

		setText(e.target.value);
	};

	const handleSubmit = (e) => {
		e.preventDefault();

		if (text.trim().length > 10) {
			const newFeedback = {
				text,
				rating,
			};

			if (feedbackEdit.isEdit) {
				updateFeedback(feedbackEdit.item.id, newFeedback);
			} else {
				addFeedback(newFeedback);
			}

			setText('');
		}
	};

	return (
		<Card>
			<form onSubmit={handleSubmit}>
				<h2>How would you rate your service with us?</h2>
				<RatingSelect select={(rating) => setRating(rating)} />
				<div className="input-group">
					<input onChange={handleTextChange} type="text" placeholder="Write a review" value={text} />
					<Button type="submit" isDisabled={btnDisabled}>
						Submit
					</Button>
				</div>
				{message && <div className="message">{message}</div>}
			</form>
		</Card>
	);
}
```

Now this should update out feedback item.
