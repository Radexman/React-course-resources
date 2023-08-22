# **Update & Delete Form Server**

Now we will refactio two remaining fucntions to the HTTP requests.

```jsx
// FeedbackContext.jsx

const deleteFeedback = async (id) => {
	if (window.confirm('Are you sure you want to delete?')) {
		await fetch(`/feedback/${id}`, {
			method: 'DELETE',
		});

		setFeedback(feedback.filter((item) => item.id !== id));
	}
};

const updateFeedback = async (id, updItem) => {
	const response = await fetch(`/feedback/${id}`, {
		method: 'PUT',
		headers: {
			'Content-Type': 'application/json',
		},
		body: JSON.stringify(updItem),
	});

	const data = response.json();

	setFeedback(feedback.map((item) => (item.id === id ? { ...item, ...data } : item)));
};
```
