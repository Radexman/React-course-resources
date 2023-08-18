# **Custom Links**

Now that we know how to create routes we will learn how to create links to those routes. We will create little question mark that will take use to the about page. Inside components directory let's create AboutIconLink component.

We can import propper icon from react-icons library

```jsx
// AboutIconLink
import { FaQuestion } from 'react-icons';

export default function AboutIconLink() {
	return (
		<div className="about-link">
			<FaQuestion size={30} />
		</div>
	);
}
```

Now let's get in on the page, in App.js import AboutIconLink component and embed it.

Next we will wrapp our link in regulat a tag and actually we shouldn't do this. a tags should only be used when redirecting user to other web page. We will use Link from the react library later.

```jsx
// AboutIconLink

import { FaQuestion } from 'react-icons';

export default function AboutIconLink() {
	return (
        <div className='about-link'>
            <a href='/about'>
                <FaQuestion size={30}/>
            <a />
        </div>
    );
}
```

Now this will work and brign us to the about page.

Let's refactor the code to work without using a tags. We need to import Link from react and wrap the icon around it, next we pass the prop with the link direction.

```jsx
// AboutIconLink.jsx

import { Link } from 'react';
import { FaQuestion } from 'react-icons';

export default function AboutIconLink() {
	return (
		<div className="about-link">
			<Link to="/about">
				<FaQuestion size={30} />
			</Link>
		</div>
	);
}
```

Okay this should work now but we still need to change a tag to Link in AboutPage

```jsx
// AboutPage

import { Link } from 'react';
import Card from '../components/shared/Card';

export default function AboutPage() {
    return (
        <Card>
            <div className='about'>
                <h1>About This Project</h1>
                <p>This is a React App to leave feedback for a product or service<p/>
                <p>Version: 1.0.0</p>
            </div>

            <p>
                <Link to='/'>Back To Home </Link>
            </p>
        </Card>
    )
}
```

Instead of passing in a string we can pass in an object.
With this syntax we can pass some additional properties like query params.

```jsx
// AboutIconLink.jsx

import { Link } from 'react';
import { FaQuestion } from 'react-icons';

export default function AboutIconLink() {
	return (
		<div className="about-link">
			<Link
				to={{
					pathname: '/about ',
					search: '?sort=name',
					hash: '#hello',
				}}
			>
				<FaQuestion size={30} />
			</Link>
		</div>
	);
}
```
