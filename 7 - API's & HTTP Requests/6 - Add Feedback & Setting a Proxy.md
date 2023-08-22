# **Add Feedback & Steeing a Proxy**

In this section and next one we will add the rest of the rquests. Also in this section we will add a proxy. We can add a proxy by going into our package.json and set it.

```json
// package.json
{
	"proxy": "http://localhost:5000"
}
```

Now we will refactor addFeecback function in our context.
We can now get rid of the uuid package.

```js
// FeedbackContext

const addFeedback = async = (newFeedback) => {
    const response = await fetch('./feedback', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(newFeedback),
    })

    const data = await response.json();

    setFeedback([data, ...feedback]);
}

```
