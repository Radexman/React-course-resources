# **Side Effects With useEffect**

Now in this section we will create actual function for changing feedback and we will also learn new react hook called useEffect.

We want the button to display on click cuttent item's rating and text back in the form component itself. From our newle created state we need to pass in to FeedbackContext.Provider value the feedbackEdit because it containe currently choosen text from the Item component.

Now we will need to get that state from the FeedbackForm component so let'd bring useContext from react inside that component and get that state.

When we want for something to happen in react we can use useEffect hook to make that happen.

## **useEffect**

This hook is called as a function and takes two arguments, callback function and array of dependencies. If we put in the array of dependencies and that changes the useEffect will run.
If we will leave the array of dependencies empty the useEffect hook will run when the component loads. In the callback function we can specify what exactly will happen when change occurs or component loads.

useEffect is a good method of making HTTP requests.

Now in our application we don't want this function to run once, we want it to run when we click on Edit Feedback Button so let's pass in to the array of dependencies the feedbackEdit state change function.

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

    const {addFeedback, feedbackEdit} = useContext(FeedbackContext);

    useEffect(() => {
        if(feedbackEdit.isEdit) {
            setBtnDisabled(false);
            setText(feedbackEdit.item.text);
            setRating(feedbackEdit.item.rating);
        }
    }, [feedbackEdit])

    const handleTextChange = (e) => {
        if (text === '') {
            setBtnDisabled(true);
            setMessage(null);
        } else if (text !== '' && text.trim().length <= 10>) {
            setBtnDisabled(true);
            setMessage('Comment has to be at least 10 charactest long');
        } else {
            setBtnDisabled(true);
            setMessage('');
        }

        setText(e.target.value);
    }


    const handleSubmit = (e) => {
        e.preventDefault();

        if (text.trim().length > 10) {
            const newFeedback = {
                text,
                rating,
            }
        }

        addFeedback(newFeedback);

        setText('');
    }

    return (
        <Card>
            <form onSubmit={handleSubmit}>
                <h2>How would you rate your service with us?</h2>
                <RatingSelect select={(rating) => setRating(rating)} />
                <div className='group-input'>
                    <input
                        onChange={handleTextChange}
                        type='text'
                        placeholder='Write a review'
                        value={text}
                    />
                    <Button type='submit' isDisabled={btnDisabled}>Submit</Button>
                </div>
                {message && <div className='message'>{message}</div>}
            </form>
        </Card>
    )
}
```

Now after these change the text of the clicked feedback item will displayd back in the form input component but the rating is catually in the differend component so let's fix that. We need to bring feedbackEdit to RatingSelect component.

```jsx
// RatingSelect.jsx

import { useState, useContext, useEffect } from 'react';
import FeedbackContext from '../context/FeedbackContext';

export default function RatingSelect({ select }) => {
    const [selected, setSelected] = useState(10);

    const { feedbackEdit } = useContext(FeedbackForm);

    useEffect(() => {
        setSelected(feedbackEdit.item.rating);
    }, [feedbackEdit])

    const handleChange = (e) => {
        setSelected(+e.currentTarget.value);
        select(+e.currentTatget.value);
    }

    return (
        <ul className='rating'>
            <li>
                <input /
                    type='radio'
                    id='num1'
                    name='rating'
                    value='1'
                    onChange={handleChange}
                    checked={selected === 1}
                >
                <label htmlFor='num1'>1</label>
            </li>
        </ul>
    )
}

```

Now this should work as expected, previous version didn't worked because the state was set in other component so essentially we needed create simmilat useEffect function inside our RatingSelect component.
