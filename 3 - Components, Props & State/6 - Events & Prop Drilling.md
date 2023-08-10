# **Events & Prop Drilling**

Now we will focuse on delete functionality which is one of the CRUD pillars. In order to delete specific item we need some kind of click event and a function that will update our global App state to exclude just clicked item. For this pourpose we needed to set id to each feedback item.

## **React Icons**

Let's create delete button which will be a simple X mark. We can import Fontawesome via CDN but React actually makes it easier to use icons with react-icons library. React icons provides:

-   Fontawesome
-   Material Icons
-   Bootstrap Icons

These are ready to use Components that can be easilly styled.

Let's install this package

```npm
npm i react-icons
```

We use component icons like any other component in React. First we need to import it and than embed it in our code. We can pass prop too.

```jsx
// FeedbackItem.jsx
import { FaTimes as Xmark } from 'react-icons/fa';
import Card from './shared/Card';

export default function FeedbackItem({ item }) {
	return (
		<Card>
			<div className="num-display">{item.rating}</div>
			<button className="close">
				<Xmark color="white" />
			</button>
			<div className="text-display">{item.text}</div>
		</Card>
	);
}

FeedbackItem.propTypes = {
	item: PropTypes.object.isRequired,
};
```

## **Events**

Now that we have some kind of visual clue for user, it's time to embed the event. Let's place click event directly into our delete button.

We can set event to a named function or we can do it directly in the onClick event.

### **Event in the onClick**

```jsx
// FeedbackItem.jsx
import { FaTimes as Xmark } from 'react-icons/fa';
import Card from './shared/Card';

export default function FeedbackItem({ item }) {
    return (
        <Card>
            <div className='num-display'>{item.rating}</div>
            <button onClick={() => console.log(item.id)} className='close'>
                <Xmark color='white'>
            </button>
            <div className='text-display'>{item.text}</div>
        </Card>
    )
}

FeedbackItem.propTypes = {
    item: PropTypes.object.isRequired,
}
```

### **Event in the separate function**

Function decalred outside JSX markup with passed argument.

```jsx
// FeedbackItem.jsx
import { FaTimes as Xmark } from 'react-icons/fa';
import Card from './shared/Card';

export default function FeedbackItem({ item }) {
    const handleClick = (id) => {
        console.log(id);
    }

    return (
        <Card>
            <div className='num-display'>{item.rating}</div>
            <button onClick={() => handleClick(item.id)} className='close'>
                <Xmark color='white'>
            </button>
            <div className='text-display'>{item.text}</div>
        </Card>
    )
}

FeedbackItem.propTypes = {
    item: PropTypes.object.isRequired,
}
```

This interaction is supposed to delete the entire item but it is impossible to manipulate global state in the local component. In order to achieve this result we need to perform action called Prop Drilling. Prop Drilling is essentially passind a prop form the App level state down to the component where the interaction is desired.

## **Prop Drilling**

Let's start prop drilling in our feedback list component, we need to simply pass in a prop.

Next we need to cath this prop inside the Item component and call handleDelete function directly in the onClick event.

```jsx
// FeedbackList.jsx

...

return (
    <div className='feedback-list'>
        {feedback.map((item) => (
            <FeedbackItem key={item.key} item={item} handleDelete={handleDelete} />
        ))}
    </div>
)

...

// FeedbackItem.jsx

export default function FeedbackItem({ item, handleDelete }){
    ...
        <button onClick={() => handleDelete(item.id)} className='close'>
            <Xmark color='white'/>
        </button>
    ...
}

```

We still need to go up one level to reach App component. We need to pass the prop higher.

```jsx
// FeedbackList.jsx

...

export default function FeedbackList({ feedback, handleDelete }) {
    ...
}

...

```

Now we can finally cath our handleDelete funtion.

```jsx
// App.js

...

export default fucntion App() {
    const [feedback, setFeedback] = useState(FeedbackData)

    return (
        <>
            <Header />
            <div className='container'>
                <FeedbackList  feedback={feedback} handleDelete={deleteFeedback}/>
            </div>
        </>
    )
}

...

```

Now we can create propper delete function that will change our's App global state. We will use filter highrt order array method to achieve that.

Also lets add small confirmation popup.

```jsx
// App.js

...

export default function App() {
    const [feedback, setFeedack] = useState(FeedbackData)

    const deleteFeedback = (id) => {
        if(window.confirm('Are you sure you want to delete this?')) {
            setFeedback(feedback.filter((item) => item.id !== id))
        }
    }

    return (
    <>
        <Header />
        <div className='container'>
            <FeedbackList  feedback={feedback} handleDelete={deleteFeedback}/>
        </div>
    </>
    )
}

...

```
