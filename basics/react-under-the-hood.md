# React Under the Hood

> How React actually works under the hood?
> Let's explore the process of how a browser renders a React application, with a special focus on the Virtual DOM.

## 🌟 What is the Virtual DOM?

Before we dive into the rendering process, we need to understand what the Virtual DOM is.

Imagine you're an architect working on a blueprint for a building. You don't make changes directly to the actual building; instead, you update your blueprint. Once you've made all your changes, you compare the new blueprint with the actual building and only make the necessary changes in the building. This is similar to how the Virtual DOM works.

The Virtual DOM is a lightweight copy of the actual DOM (Document Object Model). It's like React's own blueprint of the UI. When changes occur in a React application, React first updates this blueprint (**Virtual DOM**) rather than the actual building (**Actual DOM**). React then compares the Virtual DOM with the actual DOM and only updates the parts that have changed. This process is known as **reconciliation**.

In summary:

- **Virtual DOM**: A lightweight copy (blueprint) of the actual DOM (building).
- **Actual DOM**: The real DOM that the browser renders.
- **Reconciliation**: The process of comparing the Virtual DOM with the actual DOM and updating only the parts that have changed (like updating the actual building based on the blueprint).

## 🚀 Why use the Virtual DOM?

The Virtual DOM offers several benefits:

- **Performance Optimization**: Direct DOM manipulation is slow. The Virtual DOM minimizes these operations.
- **Batch Updates**: React can batch multiple changes together, reducing the number of updates to the real DOM.
- **Cross-Platform Consistency**: The Virtual DOM provides a consistent programming model across different platforms such as the browser, server, or mobile devices.

## 🔄 Rendering Process

### 1. Loading the HTML File

When you navigate to a React application's URL, the browser starts by requesting the main HTML file from the server.

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>My React App</title>
</head>
<body>
  <div id="root"></div>
  <!-- Bundled React script -->
  <script src="index.js"></script>
</body>
</html>
```

- The `<div id="root"></div>` is a placeholder where your React app will render.
- The `<script src="index.js"></script>` includes your bundled JavaScript code.

### 2. Loading and Parsing JavaScript

The browser then loads and parses the `main.js` file, which contains your React application code, including all components and libraries bundled together.

### 3. Executing React Code

React's entry point is typically a file like `index.js`, where you render the root component into the DOM.

```jsx
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

- `ReactDOM.render()` tells React to render the `<App />` component into the DOM element with the id root.

### 4. Creating the Virtual DOM

React creates a Virtual DOM, which is an in-memory representation of the actual DOM. This is where React keeps track of changes in the UI.

- Component Rendering: React processes your components and creates a virtual representation.

```jsx
// App.js
import React from 'react';

function App() {
  return <h1>Hello, React!</h1>;
}

export default App;
```

- The `App` component returns JSX, which is syntactic sugar for `React.createElement()` calls.
- React transforms this JSX into a Virtual DOM object.

### 5. Updating the Virtual DOM

After creating the Virtual DOM, React compares it with a snapshot of the previous Virtual DOM (if any) to determine what has changed.

- Diffing Algorithm: React uses a diffing algorithm to find the minimal number of changes between the new and old Virtual DOM.
- Reconciliation: React updates only the parts of the real DOM that have changed, improving performance.

After the Virtual DOM is updated, React applies these changes to the actual DOM, and the browser renders the updated UI.

### Wait Wait! Something's weird! 🤔

> **Question**: Why is there a `main.js` in the HTML file, but the main script is `index.js`? What's the difference between `main.js` and `index.js`?
>
> **Answer**:
>
> - `<script src="main.js"></script>`: This script tag includes the **bundled JavaScript file** that the browser will execute. This file is the output of your build process (e.g., using Webpack, Parcel, or another bundler) and contains all your React code bundled into a single file.
> - `index.js`: This is the **entry point** of your React application in your source code. It's where the React rendering process starts.

How they Relate:

1. Development vs. Production Files:
   - `index.js`: The entry point in your source code during development.
   - `main.js`: The compiled and bundled JavaScript file generated for the browser to execute.
2. Build Process:
   - When you build your React application (using tools like Webpack, Parcel, or Create React App), the bundler starts from `index.js` and processes all the imported modules and dependencies.
   - The bundler then combines everything into one or more output files, commonly named `main.js`, `bundle.js`, or something similar.
3. Including in HTML:
   - The browser doesn't understand JSX or modern JavaScript features out of the box.
   - Therefore, we include the bundled and transpiled `main.js` in the HTML file, so the browser can execute the code.

> Metaphorically, `index.js` is a Recipe 📒 for baking a cake, and `main.js` is the Baked cake 🍰 that you serve to your guests. `index.html` serves 🧑‍🍳 the cake to the guests.

Flow from Development to Production:

1. Development entry point: `index.js` (source code).
     - You write your React application code in `index.js`.

    ```jsx
        // index.js
      import React from 'react';
      import ReactDOM from 'react-dom';
      import App from './App';

      ReactDOM.render(<App />, document.getElementById('root'));
    ```

2. Bundling Process:
      - A bundler like Webpack takes `index.js` and all its dependencies.
      - Transpiles JSX and modern JavaScript into code the browser can understand.
      - Outputs a bundled file, usually named `main.js`.
3. Bundle File (`main.js`)
      - Contains your entire application code in a format suitable for browsers.
      - Included in your `index.html` file.
4. Browser Execution:
      - The browser loads `index.html`, finds the `<script src="main.js"></script>`, and executes the bundled code.
      - Your React application starts and renders components into the DOM.

## 🧩 A Simple Example of React Rendering

Let's consider a simple React component that displays a counter and increments it when a button is clicked.

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times.</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

export default Counter;
```

How it works:

1. Initial Render:
    - The component renders with `count` set to `0`.
    - The Virtual DOM is created with this state.
2. State Update:
    - When the button is clicked, `setCount(count + 1)` updates the state.
    - React creates a new Virtual DOM with `count` incremented by 1.
3. Diffing and Reconciliation:
    - React compares the new Virtual DOM with the previous one.
    - It identifies that only the text inside the `<p>` tag has changed.
4. DOM Update:
    - React updates only the specific text node in the real DOM.
    - The rest of the DOM remains untouched.

This process of updating only the necessary parts of the DOM is what makes React fast and efficient.

## 🎯 Conclusion

- React uses the Virtual DOM to optimize rendering performance.
  - The Virtual DOM is a lightweight copy of the actual DOM that React uses to track changes.
  - React updates the Virtual DOM, compares it with the actual DOM, and applies only the necessary changes.

## 🔜 What's Next?

// TODO
