DOM Manipulation & Event Handling in JavaScript

This repository contains a comprehensive guide to essential DOM methods and event-related concepts in JavaScript.

1. Selecting Elements: A Comparison

Choosing the right selection method depends on whether you need a single element or a collection, and whether that collection needs to be "live."

| Method | Selection Type | Return Type | Performance | Live? |
| --- | --- | --- | --- | --- |
| `getElementById` | ID (`#`) | Single Element | Highest | N/A |
| `getElementsByClassName` | Class (`.`) | HTMLCollection | High | Yes |
| `querySelector` | CSS Selector | Single Element | Medium | N/A |
| `querySelectorAll` | CSS Selector | Static NodeList | Medium | No |

> Note: A "Live" collection (HTMLCollection) automatically updates if the DOM changes. A "Static" collection (NodeList from `querySelectorAll`) is a snapshot and does not update.

---

2. Creating and Inserting Elements

The process follows a logical flow: Create -> Configure -> Inject.

Steps:

1. Create: Use `document.createElement('tag')`.
2. Configure: Add text with `innerText`, classes with `classList`, or attributes with `setAttribute`.
3. Inject: Use `appendChild()` (end), `prepend()` (start), or `insertBefore()`.

Code Example:

```javascript
// 1. Create the element
const newTag = document.createElement("div");

// 2. Configure it
newTag.classList.add("highlight-box");
newTag.textContent = "This was added dynamically!";

// 3. Insert into the DOM
const container = document.querySelector("#main-container");
container.appendChild(newTag);

```

---

3. Event Bubbling

Event Bubbling describes the direction in which an event moves through the DOM tree. When an event triggers on an element, it first runs the handlers on that element, then on its parent, then all the way up to the `document` object.

How it works:
If you have a `<button>` inside a `<div>`, and you click the button:

1. The button's click event fires.
2. The div's click event fires.
3. The body's click event fires.

---

4. Event Delegation

Event Delegation is a pattern that leverages Event Bubbling. Instead of adding an event listener to every single child element, you add one listener to the parent.

Why it's useful:

erformance: Uses less memory by reducing the number of listeners.
Dynamic Elements: If you add new list items via JavaScript, the parent listener will automatically handle clicks on them without needing new listeners.

Code Example:

```javascript
document.getElementById("parent-list").addEventListener("click", (event) => {
    // Check if the clicked element is an <li>
    if (event.target.tagName === 'LI') {
        console.log("List item clicked: ", event.target.innerText);
    }
});

```

---

5. preventDefault() vs. stopPropagation()

These two methods are used to control the flow of events, but they serve different purposes.

`event.preventDefault()`

Stops the default browser action associated with the event.

Use case: Preventing a form from submitting/refreshing the page or stopping a link from navigating to a URL.

 `event.stopPropagation()`

Stops the event from bubbling up the DOM tree.

Use case: Preventing a parent's click handler from firing when a child element (like a "Close" button) is clicked.

```javascript
button.addEventListener("click", (e) => {
    e.stopPropagation(); // The parent <div> will never know this was clicked.
    console.log("Button only!");
});
