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
