# **Create a Context & Provider**

Context API is a better way to manage and store our global state. It is more efficient and readable to separate out global state into contexts and then insted of passing in via props we just simply import it co propper files. With Context API the need to prop drill disappears.

First thing we are gonna do is to create context directory in out src folder and follow with creation of FeedbackContext file.

We will need to bring createContext and useState from react.

Next we can create our context and we will need to create a context provider which is a kind of wrapper for our application. With provider created and prop that will need to be passed in as a state will go under the value prop.

To pass in first feedback prop we need to create a new piece of state, simmilar to the state in App.js

```js
// FeedbackContext.js

import { createContext, useState } from 'react ';

const FeedbackContext = createContext();

export const FeedbackProvider = { children } => {
    const [feedback, setFeedback] = useState([{
        id: 1,
        text: 'This item is from context',
        rating: 10
    }]);

    return <FeebdackContext.Provider value={{
        feedback
    }}>
        {children}
        <FeedbackContext.Provider />
};

export default FeedbackContext;

```

Now to bring it in let's go to our App.js and imporn out provider. Now we will need to sorrund everything in our prider.

```jsx
// App.js

...

import { FeedbackProvider } from './context/FeedbackContext';

...

export default function App() {
    return (
        <FeedbackProvider>
            ...
        </FeedbackProvider>
    )
}
```
