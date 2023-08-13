# **Fade Animation with Framer Motion**

In this bonus section we will add Framer Motion package to add some animations to our comments.

```npm
npm i framer-motion
```

```jsx
// FeedbackList.jsx

import { motion, AnimatePresence } from 'framer-motion';

return (
	<div className="feedback-list">
        <AnimatePresence>
		{feedback.map((item) => (
            <motion.div
                key={item.id}
                initial={{opacity: 0}}
                animate={{opacity: 1}}
                exit={{opacity: 0}}
                >
			    <FeedbackItem key={item.id} item={item} handleDelete={handleDelete} />
            <motion.div />
		))}
        <AnimatePresence />
	</div>
);
```
