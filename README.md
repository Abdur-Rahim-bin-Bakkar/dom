# The Document Object Model (DOM)

The Document Object Model (DOM) is a programming interface for web documents. It represents the page so that programs can change the document structure, style, and content. The DOM represents the document as nodes and objects; that way, programming languages can interact with the page.

## 🌳 The DOM Tree

When a web page is loaded, the browser creates a Document Object Model of the page. The HTML DOM model is constructed as a tree of Objects:

- **Document**: The root node.
- **Elements**: HTML tags (e.g., `<body>`, `<a>`, `<h1>`).
- **Text**: Text inside elements.
- **Attributes**: Attributes of elements (e.g., `href`, `class`).

---

## 🔍 Selecting Elements (Get Methods)

To manipulate elements, you first need to find them. Here are the primary methods for selecting elements from the DOM:

### `getElementById(id)`
Selects a single element by its unique `id` attribute.
```javascript
const element = document.getElementById("myId");
```

### `getElementsByClassName(name)`
Returns a live HTMLCollection of all child elements which have all of the given class name(s).
```javascript
const elements = document.getElementsByClassName("myClass");
```

### `getElementsByTagName(name)`
Returns a live HTMLCollection of elements with the given tag name.
```javascript
const paragraphs = document.getElementsByTagName("p");
```

### `querySelector(selector)`
Returns the **first** element that matches a specified CSS selector(s) in the document.
```javascript
const firstItem = document.querySelector(".myClass");
const firstList = document.querySelector("ul > li");
```

### `querySelectorAll(selector)`
Returns a static NodeList representing a list of the document's elements that match the specified group of selectors.
```javascript
const allItems = document.querySelectorAll(".myClass");
```

---

## 🧭 Traversing the DOM

Once you have an element, you can navigate to its relatives.

- **`element.parentNode`**: Returns the parent node.
- **`element.childNodes`**: Returns a NodeList of child nodes (including text and comment nodes).
- **`element.children`**: Returns an HTMLCollection of child elements (excluding text and comments).
- **`element.firstChild` / `element.firstElementChild`**: Returns the first child node/element.
- **`element.lastChild` / `element.lastElementChild`**: Returns the last child node/element.
- **`element.nextSibling` / `element.nextElementSibling`**: Returns the next sibling node/element.
- **`element.previousSibling` / `element.previousElementSibling`**: Returns the previous sibling node/element.

---

## 🛠️ Manipulating Elements (Operations)

### 1. Creating Elements
- **`document.createElement(tagName)`**: Creates a new element node.
- **`document.createTextNode(text)`**: Creates a new text node.

```javascript
const newDiv = document.createElement("div");
const newText = document.createTextNode("Hello World!");
```

### 2. Adding / Inserting Elements
- **`element.appendChild(node)`**: Adds a node to the end of the list of children of a specified parent node.
- **`element.insertBefore(newNode, existingNode)`**: Inserts a node before a reference node as a child of a specified parent node.
- **`element.append(...nodes/strings)`**: Inserts a set of Node objects or DOMString objects after the last child of the Element.
- **`element.prepend(...nodes/strings)`**: Inserts a set of Node objects or DOMString objects before the first child of the Element.

### 3. Removing / Replacing Elements
- **`element.removeChild(child)`**: Removes a child node from the DOM and returns it.
- **`element.replaceChild(newChild, oldChild)`**: Replaces a child node within the given (parent) element.
- **`element.remove()`**: Removes the element from the tree it belongs to.

### 4. Modifying Content
- **`element.innerHTML`**: Gets or sets the HTML syntax describing the element's descendants. (Can parse HTML tags).
- **`element.innerText`**: Gets or sets the rendered text content of a node and its descendants. (Aware of CSS styling, e.g., hidden elements).
- **`element.textContent`**: Gets or sets the text content of a node and its descendants. (Raw text, ignores styling).

### 5. Modifying Attributes
- **`element.getAttribute(name)`**: Returns the value of a specified attribute on the element.
- **`element.setAttribute(name, value)`**: Sets the value of an attribute on the specified element.
- **`element.removeAttribute(name)`**: Removes the specified attribute from an element.
- **`element.hasAttribute(name)`**: Returns a boolean indicating if the element has the specified attribute.

### 6. Modifying Styles and Classes
- **Inline Styles**:
  ```javascript
  element.style.color = "blue";
  element.style.backgroundColor = "red";
  ```
- **ClassList API** (Preferred way to manage classes):
  - `element.classList.add("class1", "class2")`: Adds one or more classes.
  - `element.classList.remove("class1")`: Removes a class.
  - `element.classList.toggle("class")`: Toggles a class (adds if not present, removes if present).
  - `element.classList.contains("class")`: Returns true if the element has the class.

---

## 🎯 Event Handling

The DOM allows JavaScript to react to HTML events (like clicks, key presses, page load).

### `addEventListener(type, listener)`
Sets up a function that will be called whenever the specified event is delivered to the target.
```javascript
const button = document.querySelector("button");

button.addEventListener("click", function(event) {
    console.log("Button was clicked!");
    // 'event' is the Event object containing details about the action
});
```

### `removeEventListener(type, listener)`
Removes an event listener previously registered. (Requires a named function, not an anonymous one).
```javascript
function handleClick() {
    console.log("Clicked!");
}
button.addEventListener("click", handleClick);
button.removeEventListener("click", handleClick);
```

### Common Events
- **Mouse**: `click`, `dblclick`, `mousedown`, `mouseup`, `mousemove`, `mouseover`, `mouseout`
- **Keyboard**: `keydown`, `keyup`, `keypress`
- **Form**: `submit`, `change`, `focus`, `blur`, `input`
- **Document/Window**: `DOMContentLoaded`, `load`, `resize`, `scroll`

---

## 🚀 Advanced Event Handling

### Event Propagation (Bubbling & Capturing)
When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors. This is called **Event Bubbling**.
- **`event.stopPropagation()`**: Stops the event from bubbling up the DOM tree.
- **`event.preventDefault()`**: Prevents the browser's default behavior (like following a link or submitting a form).

### Event Delegation
Instead of adding an event listener to every single child element (which is bad for performance and memory), you can add a single event listener to a parent element and use `event.target` to figure out which child triggered the event.

```javascript
const list = document.querySelector("ul");

list.addEventListener("click", function(event) {
    if (event.target.tagName === "LI") {
        console.log("List item clicked:", event.target.innerText);
    }
});
```

---

## 💾 Data Attributes (Dataset)

HTML5 allows you to store extra information in standard HTML elements without other hacks like non-standard attributes. These are prefixed with `data-`.

```html
<article id="electric-cars" data-columns="3" data-index-number="12314">
  ...
</article>
```

You can access these in JavaScript using the `dataset` property:
```javascript
const article = document.getElementById("electric-cars");

console.log(article.dataset.columns); // "3"
console.log(article.dataset.indexNumber); // "12314" (CamelCase is used in JS)

// Updating a data attribute
article.dataset.columns = "4";
```

---

## ⚡ Performance: Reflow, Repaint, and DocumentFragment

### Reflow and Repaint
Every time you change the DOM, the browser has to recalculate styles and positions (**Reflow**) and redraw the pixels on the screen (**Repaint**). Doing this too often in a loop will slow down your application.

### DocumentFragment
To avoid triggering multiple reflows, use a `DocumentFragment`. It is a lightweight version of a Document that stores DOM structure in memory. Since it's not attached to the active DOM tree, changes made to it don't affect the document or cause reflow.

```javascript
const list = document.getElementById("myList");
const fragment = document.createDocumentFragment();
const fruits = ['Apple', 'Banana', 'Mango'];

fruits.forEach(fruit => {
    const li = document.createElement("li");
    li.textContent = fruit;
    fragment.appendChild(li); // Appends to memory, no reflow
});

// Append the fragment to the DOM all at once (triggers 1 reflow)
list.appendChild(fragment); 
```

---

## 🏗️ Understanding Node Types

Everything in the DOM is a **Node**, but not all nodes are **Elements**. There are 12 node types, but here are the most common ones you'll interact with:

1. **`Node.ELEMENT_NODE` (1)**: An Element node such as `<p>` or `<div>`.
2. **`Node.TEXT_NODE` (3)**: The actual text inside an Element or Attribute.
3. **`Node.COMMENT_NODE` (8)**: An HTML comment `<!-- ... -->`.
4. **`Node.DOCUMENT_NODE` (9)**: The root node of the document.
5. **`Node.DOCUMENT_FRAGMENT_NODE` (11)**: A lightweight document object.

You can check a node's type using the `nodeType` property:
```javascript
const paragraph = document.querySelector("p");
console.log(paragraph.nodeType === Node.ELEMENT_NODE); // true
```

---

## 🌐 BOM vs DOM

While learning the DOM, you will often hear about the BOM.
- **DOM (Document Object Model)**: Deals with the web page content and structure (`document`).
- **BOM (Browser Object Model)**: Deals with browser components outside of the document itself (`window`). This includes `window.innerHeight`, `window.location`, `navigator`, `localStorage`, and `setTimeout`.

The `document` object is actually a property of the `window` object (`window.document`).
