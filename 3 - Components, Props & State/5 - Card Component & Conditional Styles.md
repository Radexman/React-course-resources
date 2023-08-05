# **Card Component & Conditional Styles**

## **Styled Component**

In this segment we will create a card component that can be used in multiple places and can render conditional syles. Let's start with crating new directory incide components and name it 'shared'.

Next create Card component and scaffold it.

```jsx
// Card.jsx

export default function Card() {
	return <div>Card</div>;
}
```

Import Card component inside FeedbackItem and wrap two inner divs around it.

```jsx
// FeedbackItem.jsx

import Card from './shared/Card';

export default function FeedbackItem({ item }) {
	return (
		<Card>
			<div className="num-display">{item.rating}</div>
			<div className="text-display">{item.text}</div>
		</Card>
	);
}
```

To get what markup is inside Card component we need do destructure children prop from it and add class.

```jsx
// Card.jsx

export default function Card({ children }) {
	return <div className="card">{children}</div>;
}
```

## **Conditional Styling**

We can pass a bool prop 'reverse' for different styles.

```jsx
// FeedbackItem.jsx

import Card from './shared/Card';

export default function FeedbackItem({ item }) {
	return (
		<Card reverse={true}>
			<div className="num-display">{item.rating}</div>
			<div className="text-display">{item.text}</div>
		</Card>
	);
}
```

Next in the Card component we need to cath that prop and write conditional styles.

```jsx
// Card.jsx

export default function Card({ children, reverse }) {
	return <div className="card">{children}</div>;
}
```

There are two ways of doing condtional styling changing class or changing styles.

### **Conditional Class**

We need to have propper css styles in place for this method to work.

```css
/* Index.css */

.card {
	background-color: #fff;
	color: #333;
	border-radius: 15px;
	padding: 40px 50px;
	margin: 20px 0;
	position: relative;
}

.card.reverse {
	background-color: rgba(0, 0, 0, 0.4);
	color: #fff;
}
```

Back in our Card component if we have card and reverse classes the Card will be dark with white font.

We only want to card to be dark when reverse is true.
Instead of string we open curly braces and inside backticks we write our original class because we need it to be there all the time. Next we open template string and using logical AND operator, the value on the right will be assigned if the expression is evaluated positvely.

```jsx
// Card.jsx

export default function Card({ children, reverse }) {
	return <div className={`card ${reverse && 'reverse'}`}>{children}</div>;
}
```

### **Conditional Style**

Here instead of using classes we write our style diectly inside style tag with double set of curly braces. Next we specify css properties and we need to assign ternary operator to evaluate outcome of the expression.

```jsx
// Card.jsx

export default function Card({ item, children }) {
	return (
		<div
			style={{
				backgroundColor: reverse ? 'rgba(0,0,0,0.4)' : '#ffffff',
				color: reverse ? '#ffffff' : '#000000',
			}}
		>
			{children}
		</div>
	);
}
```

Our conditional styling can be used as default prop too. Delete prop passed in the card. Next we set Card default props.

```jsx
// Card.jsx

Card.defaultProps = {
    reverse: true;
}
```

In previous modules we didn't added PropTypes so we can do that now.

There is a neat snippet for importing PropTypes

```jsx
// Card.jsx

impt = import PropTypes from = 'prop-types';

Card.propTypes = {
    children: PropTypes.node.isRequired,
    reverse: PropTypes.bool
}
```

PropTypes in other componets and arrayOf prop type. Remember to import prop types in each component.

```jsx
// FeedbackItem.jsx
FeedbackItem.propTypes = {
	item: PropTypes.object.isRequired,
};

// FeedbackList.jsx
FeedbackList.propTypes = {
	feedback: PropTypes.arrayOf(
		PropTypes.shape({
			id: PropTypes.number.isRequired,
			rating: PropTypes.number.isRequired,
			text: PropTypes.string.isRequired,
		})
	),
};
```

We can set the shape of the array much like in TypeScript.
