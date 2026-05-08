# Short Response: Intro to React, Components, and useState

Answer each question below. Write in complete sentences (3–5 per answer).

---

## Question 1 — Components and JSX

What is a React component, and what is JSX? Explain how JSX differs from plain HTML. Use a brief code example to support your answer.

**Your answer:**

A **React component** is a JavaScript function that returns UI, describing what should appear on screen. **JSX** is a syntax extension that lets you write HTML-like markup directly inside JavaScript. Unlike plain HTML, JSX is not valid in a browser, it needs to be compiled into regular JavaScript first. For example, `<p>Hello</p>` in JSX becomes `React.createElement('p', null, 'Hello')`.

---

## Question 2 — The Build Step and Vite

A browser cannot run a `.jsx` file directly. Why not? Explain the role of a build step and what it means to "compile" code in simple terms.

**Your answer:**

Browsers only understand plain HTML, CSS, and JavaScript, they can't read `.jsx` files or modern JS syntax directly. A build step is a process that transforms your code into something browsers can run. "Compiling" means converting your developer-friendly code into standard JavaScript. Vite handles this by processing your files and bundling them into a `dist` folder ready for the browser.

---

## Question 3 — useState

What does `useState` return, and what are the two things you get back from it? Describe how to use those values to render data and to update that data.

**Your answer:**

`useState` returns an array with two things, the current state value and a setter function to update it. You use the value to render data in your JSX, like `<p>{count}</p>`. You call the setter in response to events, like `onClick={() => setCount(count + 1)}`, which triggers a re-render with the new value.

---

## Question 4 — Lifting State Up

What does it mean to "lift state up," and when is it necessary? Use a concrete example.

**Your answer:**

**Lifting state** up means moving state to the nearest common parent when two sibling components both need access to it. It's necessary when one sibling needs to read a value that another sibling changes. For example, if `GreetingDisplay` needs to show the selected language and `LanguageButtons` needs to update it, `App` owns the state and passes it down to both as props.

---

## Question 5 — Bug Fix

The component below has a bug. When the user clicks "Add Cherries," the list never updates on screen. Identify what is wrong, write the corrected code, and explain **why** the original code fails in React.

```jsx
const ShoppingList = () => {
  const [items, setItems] = useState(['apples', 'bananas']);

  const addItem = () => {
    items.push('cherries');
    setItems(items);
  };

  return (
    <>
      <ul>
        {items.map((item, i) => <li key={i}>{item}</li>)}
      </ul>
      <button onClick={addItem}>Add Cherries</button>
    </>
  );
};
```

**Your answer:**

The bug is that `items.push()` mutates the existing array, so when `setItems(items)` is called, React sees the same array reference and skips re-rendering. Instead we should create a new array:

```js
const addItem = () => {
  setItems([...items, 'cherries']);
};
```

React determines whether to re-render by checking if state changed, if the reference is identical, it assumes nothing changed and does nothing.

---
