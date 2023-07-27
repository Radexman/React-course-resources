# **React & Tailwind Css**

In order to use Tailwind CSS utility classes we need to instal Tailwind in our project.

## **Default Tailwind CSS Config**

Install tailwindcss via npm, and then run the init command to generate your tailwind.config.js file.

```bash
npm install -D tailwindcss
npx tailwindcss init
```

Add the paths to all of your template files in your tailwind.config.js file

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
	content: ['./src/**/*.{js,jsx,ts,tsx}'],
	theme: {
		extend: {},
	},
	plugins: [],
};
```

Add the @tailwind directives for each of Tailwind’s layers to your ./src/index.css file.

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## **Tailwind + Prettier**

To get started, just install prettier-plugin-tailwindcss as a dev-dependency.

```bash
npm install -D prettier prettier-plugin-tailwindcss
```

## **Environment Setup with Emmet & IntelliSense**

In order to make writing Tailwind classes even better fallow these steps to configure VS Code.

Then add the plugin to your Prettier config:

```js
// prettier.config.js
module.exports = {
	plugins: ['prettier-plugin-tailwindcss'],
};
```

Install Tailwind IntelliSense extension in VS Code. For better hints add follownig rules to your JSON Settings

```json
"files.associations": {
  "*.css": "tailwindcss"
},
"editor.quickSuggestions": {
  "strings": true
}
```

Happy Styling!
