# **Rating Selection Component**

In this part of out feedback application we will create radio input buttons that will be displaying ratings that user can send back.

Let's add another piece of state to our FeedbackForm because as I mentioned earlier, every form input should have each own separate piece of state. Also import rating compoent and embed it to our form.

```jsx
// FeedbackForm.jsx
import { useState } from 'react';
import Card from './shared/Card';
import Button from './shared/Button';
import RatingSelect from './RatingSelect';

export default function FeedbackForm() {
	const [text, setText] = useState('');
	const [rating, setRating] = useState(10);
	const [btnDisabled, setBtnDisabled] = useState(true);
	const [message, setMessage] = useState('');

	const handleTextChange = (e) => {
		if (text === '') {
			setBtnDisabled(true);
			setMessage(null);
		} else if (text !== '' && text.trim().length <= 10) {
			setBtnDisabled(true);
			setMessage('Review has to be at least 10 charcters long');
		} else {
			setBtnDiabled(false);
			setMessage(null);
		}

		setText(e.target.value);
	};

	return (
		<Card>
			<form>
				<h2>How would you rate your service with us?</h2>
				<RatindSelect />
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

Now let's create that rating component and bring it to FeedbackForm. Create piece of state that will hold selected rating.

The rating imput itself will be a unordered list that will contain radio buttons. The styling to achieve desired effect is in the main css file enclosed to the main course.
We need to set the state and than handle event and cath the input. Now we can pass in the rating as a prop.

```jsx
// RatingSelect.jsx
import { useState } from 'react';

export default function RatingSelect({ select }) {
	const [selected, setSelected] = useState(10);

    const handleChange = (e) => {
        setSelected(+e.currentTarget.value)
        select(+e.currentTardet.value)
    }

	return (
     <ul className='rating'>
        <li>
            <input
             type='radio'
             id='num1'
             name='rating'
             value='1'
             onChange={handleChange}
             checked={selected === 1}
             />
             <label htmlFor='num1'>1<label />
        </li>
        <li>
            <input
             type='radio'
             id='num2'
             name='rating'
             value='2'
             onChange={handleChange}
             checked={selected === 2}
            />
            <label htmlFor='num2'>2</label>
        </li>
        <li>
            <input
             type='radio'
             id='num3'
             name='rating'
             value='3'
             onChange={handleChange}
             checked={selected === 3}
            />
            <label htmlFor='num3'>3</label>
        </li>
        <li>
            <input
             type='radio'
             id='num4'
             name='rating'
             value='4'
             onChange={handleChange}
             checked={selected === 4}
            />
            <label htmlFor='num4'>4</label>
        </li>
        <li>
            <input
             type='radio'
             id='num5'
             name='rating'
             value='5'
             onChange={handleChange}
             checked={selected === 5}
            />
            <label htmlFor='num5'>5</label>
        </li>
        <li>
            <input
             type='radio'
             id='num6'
             name='rating'
             valur='6'
             onChange={handleChange}
             checked={selected === 6}
            />
            <label htmlFor='num6'>6</label>
        </li>
        <li>
            <input
             type='radio'
             id='num7'
             name='rating'
             value='7'
             onChange={handleChange}
             checked={selected === 7}
            />
            <label htmlFor='num7'>7</label>
        </li>
        <li>
            <input
             type='radio'
             id='num8'
             name='rating'
             value='8'
             onChange={handleChange}
             checked={selected === 8}
            />
            <label htmlFor='num8'>8</label>
        </li>
        <li>
            <input
             type='radio'
             id='num9'
             name='rating'
             value='9'
             onChange={handleChange}
             checked={selected === 9}
            />
            <label htmlFor='num9'>9</label>
        </li>
        <li>
            <input
             type='radio'
             id='num10'
             name='rating'
             value='10'
             onChange={handleChange}
             checked={selected === 10}
            />
            <label htmlFor='num10'>10</label>
        </li>
    </ul> );
}
```

Now we will pass in a prop to the embedded component in the FeedbackForm component.

```jsx
// FeedbackForm.jsx

...
    <RatingSelect select={(rating) => setRating(rating)} />
...

```
