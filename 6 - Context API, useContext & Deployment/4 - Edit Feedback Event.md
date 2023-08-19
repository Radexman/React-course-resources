# **Edit Feedback Event**

So now that we refactored our code to the context it's time to complete the CRUD functionality of our application, the only one aspect that is missing is Update so let's get to work.

We will need to add another piece of state for the update functionality. Let's start with adding propper icon to our FeedbackItem component that will be responsible for updating comment.

```jsx
// FeedbackItem.jsx

import { FaTimes as Xmark, FaEdit } from 'react-icons/fa';
import { useContext } from 'react';
import PropTypes from 'prop-types';
import Card from './shared/Card';
import FeedbackContex from '../context/FeedbackContext';

export default function FeedbackItem({ item }) {
	const { deleteFeedback } = useContext(FeedbackContext);

	return (
		<Card>
			<div className="num-dispaly">{item.rating}</div>
			<button onClick={() => deleteFeedback(item.id)} className="close">
				<Xmark color="purple" />
			</button>
			<button className="edit">
				<FaEdit color="purple" />
			</button>
			<div className="text-display">{item.text}</div>
		</Card>
	);
}

FeedbackItem.propTypes = {
	item: PropTypes.object.isRequired,
};
```

So now that we created propper button we need to create function responsible for feedback change in our context and new piece of state.

New piece of state will be edited on button click that we created inside of FeedbackItem, let's create it.

Now in order to use newly created function we need to pass it to FeedbackProvider value params.

```js
// FeedbackContex.js

import { v4 as uuid4 } from 'uuid';
import { createContext, useState } from 'react';

const FeedbackContext = createContext();


export const FeedbackProvider = ({children}) => {
    const [feedback, setFeedback] = useState([
        {
            id: 1,
            text: 'This is feedback item One',
            rating: 10,
        }
        {
            id: 2,
            text: 'This is feedback item Two',
            rating: 9
        }
        {
            id: 3,
            text: 'This is feedback item Three',
            rating: 7,
        }
    ]);

    const [feedbackEdit, setFeedbackEdit] = useState({
        item: {},
        isEdit: false
    })

    // Add new feedback item
    const addFeedback = (newFeedback) => {
        newFeedback.id = uuid4();
        setFeedback([newFeedback, ...feedback]);
    }

    // Delete feedback item
    const deleteFeedback = (id) => {
        if(window.confirm('Are you sure you want to delete?')) {
            setFeedback(feedback.filter((item) => item.id !== id))
        }
    }

    // Set item to be updated
    const editFeedback = (item) => {
        setFeedbackEdit({
            item,
            isEdit: true
        })
    }

    return (
        <FeedbackContext.Provider value={{
            feedback,
            addFeedback,
            deleteFeedback,
            editFeedback
        }}>
            {children}
        </FeedbackContext.Provider>
    )
}
```

Now that our new context and function are created we can add event to the update button. First we need to bring that functionality from the useContext Hook.

```jsx
// FeedbackItem.jsx

import { FaTimes as Xmark, FaEdit } from 'react-icons/fa';
import { useContext } from 'react';
import PropTypes from 'prop-types';
import Card from './shared/Card';
import FeedbackContex from '../context/FeedbackContext';

export default function FeedbackItem({ item }) {
	const { deleteFeedback, editFeedback } = useContext(FeedbackContext);

	return (
		<Card>
			<div className="num-dispaly">{item.rating}</div>
			<button onClick={() => deleteFeedback(item.id)} className="close">
				<Xmark color="purple" />
			</button>
			<button onClick={() => editFeedback(item)} className="edit">
				<FaEdit color="purple" />
			</button>
			<div className="text-display">{item.text}</div>
		</Card>
	);
}

FeedbackItem.propTypes = {
	item: PropTypes.object.isRequired,
};
```

Now nothing will be displayed in the UI yet but when we check out out React Dev Tools we will see new piece of state upon buttin click.
