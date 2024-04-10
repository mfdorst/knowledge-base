# Set up a project using SolidJS, Vite and Tailwind CSS

See <https://tailwindcss.com/docs/guides/solidjs>

1. Create your project

```bash
npx degit solidjs/templates/js my-project
cd my-project
```

2. Install Tailwind CSS

```bash
npm install -D tailwindcss postcss autoprefixer
# Generate `tailwind.config.js` and `postcss.config.js`
npx tailwindcss init -p
```

3. Configure your template paths

Edit `tailwind.config.js`:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

4. Add Tailwind directives to your CSS

Add to `src/index.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

5. Use Tailwind classes in your app

Edit `src/App.jsx`:

```js
export default function App() {
  return (
    <h1 class="text-3xl font-bold underline">
      Hello world!
    </h1>
  )
}
```

6. Build and serve your project

```bash
npm run dev
```
