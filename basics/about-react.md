# 🚀 About React

## ❓ What is React?

> **React** is a JavaScript library for building user interfaces. It was created by Facebook.

## ⏳ Before React was created

> Before React was created, web development faced several challenges, such as:
>
> - **Complexity**: Web development was complex because of the lack of a good way to manage the state of the application.
> - **Performance**: Web development was slow because of the lack of a good way to update the DOM (Document Object Model).
> - **Reusability**: Web development was not reusable because of the lack of a good way to create reusable components.

## 🤔 Why do I need to learn React?

Let's compare creating a simple web application using only HTML, CSS, and JavaScript with creating the same web application using React.

### 🚫 Without React

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Counter without React</title>
</head>
<body>
    <h1>Counter: <span id="count">0</span></h1>
    <button id="increment">Increment</button>
    <button id="decrement">Decrement</button>

    <script>
        let count = 0;
        const countDisplay = document.getElementById('count');
        const incrementBtn = document.getElementById('increment');
        const decrementBtn = document.getElementById('decrement');

        function updateDisplay() {
            countDisplay.textContent = count;
        }

        incrementBtn.addEventListener('click', () => {
            count++;
            updateDisplay();
        });

        decrementBtn.addEventListener('click', () => {
            count--;
            updateDisplay();
        });
    </script>
</body>
</html>
```

> As you can see, the code above is not reusable, and it is hard to manage the state of the application.
> Imagine, if the application is more complex, the code will be more complex 🤯

### ✅ With React

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);

  return (
    <div>
      <h1>Counter: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
};

export default Counter;
```

> Of course, there should be a setup to use React, but the code above is more readable 🤓, reusable ♻️, and easy to manage 🛠️ the state of the application.

## 🔜 What's next?

- [React Under the Hood](./react-under-the-hood.md)
- [Check other topics!](../README.md)
