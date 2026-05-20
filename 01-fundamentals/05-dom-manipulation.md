# 1.5 DOM Manipulation

The Document Object Model (DOM) is the browser's representation of a webpage. JavaScript can manipulate it to create interactive pages.

## Selecting Elements

### Older Methods (Still Used)

```javascript
// By ID
const header = document.getElementById("header");

// By Class
const buttons = document.getElementsByClassName("btn");

// By Tag
const divs = document.getElementsByTagName("div");
```

### Modern Methods (Recommended)

```javascript
// Select first matching element
const element = document.querySelector("#header");
const button = document.querySelector(".btn");
const div = document.querySelector("div");

// Select all matching elements
const buttons = document.querySelectorAll(".btn");
const items = document.querySelectorAll("li");

// Loop through NodeList
buttons.forEach(btn => {
  console.log(btn.textContent);
});
```

### Selectors

```javascript
document.querySelector("#header");           // ID
document.querySelector(".btn");             // Class
document.querySelector("div");              // Tag
document.querySelector("div.container");    // Tag with class
document.querySelector("[type='submit']");  // Attribute
```

---

## Creating & Modifying Elements

### Creating Elements

```javascript
const newDiv = document.createElement("div");
const newParagraph = document.createElement("p");
const newButton = document.createElement("button");

// Set content
newDiv.textContent = "Hello World";
newDiv.innerHTML = "<strong>Bold Text</strong>";

// Set attributes
newButton.setAttribute("type", "submit");
newButton.id = "submitBtn";
newButton.className = "btn btn-primary";

// Add to page
document.body.appendChild(newDiv);
```

### Adding to DOM

```javascript
const container = document.querySelector(".container");
const newElement = document.createElement("p");
newElement.textContent = "New paragraph";

// Add as last child
container.appendChild(newElement);

// Add at specific position
const firstChild = container.firstChild;
container.insertBefore(newElement, firstChild);

// Add as sibling
const sibling = document.querySelector(".item");
sibling.insertAdjacentHTML("afterend", "<p>New sibling</p>");
```

### Modifying Content

```javascript
const heading = document.querySelector("h1");

// Change text
heading.textContent = "New Title";

// Change HTML
heading.innerHTML = "<em>Emphasized Title</em>";

// Get content
console.log(heading.textContent);
console.log(heading.innerHTML);
```

### Modifying Attributes

```javascript
const link = document.querySelector("a");

// Set attribute
link.setAttribute("href", "https://example.com");
link.setAttribute("target", "_blank");

// Get attribute
console.log(link.getAttribute("href"));

// Remove attribute
link.removeAttribute("target");

// Direct property access
link.href = "https://example.com";
link.target = "_blank";
```

---

## Working with Classes

```javascript
const element = document.querySelector(".box");

// Add class
element.classList.add("active");
element.classList.add("highlighted", "large"); // Multiple

// Remove class
element.classList.remove("active");
element.classList.remove("active", "highlighted"); // Multiple

// Toggle class
element.classList.toggle("dark-mode");

// Check if has class
if (element.classList.contains("active")) {
  console.log("Element is active");
}

// Replace class
element.classList.replace("old-class", "new-class");
```

---

## Modifying Styles

### Inline Styles

```javascript
const box = document.querySelector(".box");

// Set styles
box.style.backgroundColor = "blue";
box.style.color = "white";
box.style.padding = "20px";
box.style.borderRadius = "5px";

// Get styles (only inline)
console.log(box.style.backgroundColor);

// Multiple styles
const styles = {
  backgroundColor: "green",
  color: "white",
  padding: "10px"
};

Object.assign(box.style, styles);
```

### CSS Classes (Better Approach)

```css
/* style.css */
.highlight {
  background-color: yellow;
  color: black;
  padding: 10px;
}
```

```javascript
const element = document.querySelector("p");
element.classList.add("highlight");
```

---

## Event Listeners

### Adding Event Listeners

```javascript
const button = document.querySelector("button");

// Click event
button.addEventListener("click", function(event) {
  console.log("Button clicked!");
  console.log(event);
});

// Arrow function
button.addEventListener("click", (e) => {
  console.log("Clicked");
});

// Multiple events
button.addEventListener("mouseenter", () => {
  button.style.backgroundColor = "blue";
});

button.addEventListener("mouseleave", () => {
  button.style.backgroundColor = "";
});
```

### Common Events

```javascript
const input = document.querySelector("input");
const button = document.querySelector("button");
const form = document.querySelector("form");

// Input events
input.addEventListener("input", (e) => {
  console.log(e.target.value); // Current value
});

input.addEventListener("change", (e) => {
  console.log("Value changed:", e.target.value);
});

input.addEventListener("focus", () => {
  console.log("Input focused");
});

input.addEventListener("blur", () => {
  console.log("Input lost focus");
});

// Form event
form.addEventListener("submit", (e) => {
  e.preventDefault(); // Stop default behavior
  console.log("Form submitted");
});

// Keyboard events
document.addEventListener("keydown", (e) => {
  console.log(e.key); // 'a', 'Enter', 'Escape', etc.
});
```

### Event Object Properties

```javascript
button.addEventListener("click", (e) => {
  console.log(e.target);        // Element that triggered event
  console.log(e.type);          // 'click'
  console.log(e.x, e.y);        // Mouse position
  console.log(e.timeStamp);     // When event occurred
  e.preventDefault();           // Stop default action
  e.stopPropagation();          // Stop event bubbling
});
```

---

## Practical Examples

### Example 1: Simple Todo List

```html
<input id="todoInput" placeholder="Enter todo..." />
<button id="addBtn">Add</button>
<ul id="todoList"></ul>
```

```javascript
const input = document.querySelector("#todoInput");
const btn = document.querySelector("#addBtn");
const list = document.querySelector("#todoList");

function addTodo() {
  const text = input.value;
  if (text.trim() === "") return;
  
  const li = document.createElement("li");
  li.textContent = text;
  
  const deleteBtn = document.createElement("button");
  deleteBtn.textContent = "Delete";
  deleteBtn.addEventListener("click", () => {
    li.remove();
  });
  
  li.appendChild(deleteBtn);
  list.appendChild(li);
  
  input.value = "";
}

btn.addEventListener("click", addTodo);
input.addEventListener("keypress", (e) => {
  if (e.key === "Enter") addTodo();
});
```

### Example 2: Theme Switcher

```javascript
const toggle = document.querySelector("#themeToggle");
const body = document.body;

// Check saved theme
const savedTheme = localStorage.getItem("theme") || "light";
body.classList.add(savedTheme);

toggle.addEventListener("click", () => {
  const isDark = body.classList.contains("dark");
  
  if (isDark) {
    body.classList.remove("dark");
    body.classList.add("light");
    localStorage.setItem("theme", "light");
  } else {
    body.classList.remove("light");
    body.classList.add("dark");
    localStorage.setItem("theme", "dark");
  }
});
```

### Example 3: Form Validation

```javascript
const form = document.querySelector("form");

form.addEventListener("submit", (e) => {
  e.preventDefault();
  
  const name = form.querySelector("[name='name']").value;
  const email = form.querySelector("[name='email']").value;
  
  if (name.trim() === "") {
    alert("Name is required");
    return;
  }
  
  if (!email.includes("@")) {
    alert("Invalid email");
    return;
  }
  
  console.log("Form valid", { name, email });
  // Submit data...
});
```

---

## ✅ Practice Exercises

### Exercise 1: Button Click Counter
```javascript
// Create a button and paragraph
// Count clicks and display in paragraph
```

### Exercise 2: Change Background Color
```javascript
// Create buttons for different colors
// Change page background on click
```

### Exercise 3: Hide/Show Element
```javascript
// Create toggle button to show/hide element
```

---

## 🎯 Key Takeaways

✅ Use querySelector for modern element selection  
✅ Create elements with createElement  
✅ Use classList for CSS classes  
✅ addEventListener for interactive pages  
✅ Prevent default with preventDefault()  

---

**Next:** [Phase 2: Intermediate JavaScript](../02-intermediate/README.md)