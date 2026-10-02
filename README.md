## DOM Selection & Manipulation

**What the DOM is**

DOM (Document Object Model) is the browser's live, tree-like representation of your HTML page. Every tag becomes an object (a "node") that JavaScript can read and change. JS doesn't edit your `.html` file; it edits this in-memory version, and the page updates instantly.

```
document
 └── html
      ├── head
      │    └── title
      └── body
           ├── h1
           └── p
```

`document` is the global object that is the entry point to everything.

**Connecting JS to HTML**

```html
<body>
``````html
  <h1 id="title">Hello</h1>
  <p class="text">First paragraph</p>
  <p class="text">Second paragraph</p>

  <script src="script.js"></script>
</body>
```

Put the `<script>` at the end of `<body>`, so the elements exist before JS tries to select them. Alternative: put it in `<head>` with `defer`:

```html
<script src="script.js" defer></script>
```

---

**Selecting elements**

By ID (returns one element):

```jsx
const title = document.getElementById("title");
```

By class / tag (return multiple, as a collection):

```jsx
const texts = document.getElementsByClassName("text");
const paras = document.getElementsByTagName
```**Modern way: `querySelector` / `querySelectorAll`**

Uses CSS selector syntax, the same `#id`, `.class`, `tag` from the CSS week.

```jsx
const title = document.querySelector("#title");     // first match only
const firstText = document.querySelector(".text");  // first .text element
const allTexts = document.querySelectorAll(".text"); // ALL matches (NodeList)
const link = document.querySelector("nav a");        // any valid CSS selector works
```

`querySelector` returns the first match (or `null` if none). `querySelectorAll` returns all matches.

**Looping over multiple elements**

```jsx
const allTexts = document.querySelectorAll(".text");

allTexts.forEach(function (item) {
  console.log(item);
});

// or
for (let item of allTexts) {
  console.log(item);
}
```

A `NodeList` looks like an array but isn't fully one. `forEach` and `for...of` work; some array methods don't.

---

**Changing content**

`textContent`: plain text only

```jsx
const title = document.querySelector("#title");
console.log(title.textContent);         // read → "Hello"
title.textContent = "Welcome to JS";    // change
```

`innerHTML`: parses HTML tags

```jsx
const box = document.querySelector("#box");
box.innerHTML = "<strong>Bold text</strong>";
```

`textContent` vs `innerHTML`:`textContent` vs `innerHTML`:

- `textContent` treats everything as plain text, so it's safe
- `innerHTML` renders tags, but putting user-typed input into it is a security risk (XSS). Prefer `textContent` unless you truly need HTML

---

**Changing attributes**

```html
<img id="pic" src="cat.jpg" alt="Cat">
<a id="link" href="https://google.com">Google</a>
```

```jsx
const pic = document.querySelector("#pic");
pic.src = "dog.jpg";
pic.alt = "A dog";

const link = document.querySelector("#link");
link.href = "https://github.com";
```

General methods that work on any attribute:

```jsx
pic.getAttribute("src");            // read
pic.setAttribute("alt", "New alt"); // set
pic.removeAttribute("alt");         // remove
```

---

**Changing styles**

Inline styles via `.style` (property names become camelCase):

```jsx
const title = document.querySelector("#title");
title.style.color = "red";
title.style.backgroundColor = "yellow";   // background-color → backgroundColor
title.style.fontSize = "32px";            // font-size → fontSize
```

Better approach: toggle CSS classes with `classList`

```css
.highlight {
  background-color: yellow;
  color: black;
}
```

```jsx
title.classList.add("highlight");
title.classList.remove("highlight");
title.classList.toggle("highlight");    // adds if missing, removes if present
title.classList.contains("highlight");  // true / false
```

Keep the styling in CSS and let JS just switch classes on and off. It's cleaner than writing many `.style` lines.

---

**Creating and adding elements**

```jsx
const list = document.querySelector("#myList");   // an existing <ul>

const newItem = document.createElement("li");     // 1. create
newItem.textContent = "New item";                 // 2. give it content
list.appendChild(newItem);                        // 3. add to the page
```

Creating an element does nothing visible until you attach it to something already on the page.

Other ways to insert:```jsx
title.classList.add("highlight");
title.classList.remove("highlight");
title.classList.toggle("highlight");    // adds if missing, removes if present
title.classList.contains("highlight");  // true / false
```

Keep the styling in CSS and let JS just switch classes on and off. It's cleaner than writing many `.style` lines.

---

**Creating and adding elements**

```jsx
const list = document.querySelector("#myList");   // an existing <ul>

const newItem = document.createElement("li");     // 1. create
newItem.textContent = "New item";                 // 2. give it content
list.appendChild(newItem);                        // 3. add to the page
```

Creating an element does nothing visible until you attach it to something already on the page.

Other ways to insert:

```jsx
list.append(newItem);      // add at the end (also accepts text)
list.prepend(newItem);     // add at the start
```

**Removing elements**

```jsx
newItem.remove();   // removes the element from the page
```

**Navigating between elements (quick intro)**

```jsx
const item = document.querySelector("li");

item.parentElement;          // the <ul>
item.nextElementSibling;     // next <li>
item.previousElementSibling; // previous <li>
list.children;               // all child elements
```

---

**Putting it together, a small example**

```html
<h1 id="title">Hello</h1>
<ul id="list">
  <li>HTML</li>
  <li>CSS</li>
</ul>
<script src="script.js"></script>
```

```jsx
const title = document.querySelector("#title");
title.textContent = "My Skills";
title.style.color = "teal";

const list = document.querySelector("#list");
const newItem = document.createElement("li");
newItem.textContent = "JavaScript";
list.appendChild(newItem);
```

**Common mistakes**

- Script placed before the HTML elements (or no `defer`), so `querySelector` returns `null` and you get "Cannot read properties of null"
- Using `querySelector` when you meant `querySelectorAll`, and only the first element changes
- Writing `.style.background-color` instead of `.style.backgroundColor`
- Forgetting `#` for IDs or `.` for classes inside `querySelector`
- Calling `.style` or `.textContent` directly on a `NodeList` instead of looping through it
- Creating an element with `createElement` but never appending it, so nothing shows up
- Using `innerHTML` with user-provided content

**Small practice task**```html
<!-- Setup: a page with an h1, three <p class="para"> elements,
     an <img>, and an empty <ul id="list"> -->
```

```jsx
// 1. Select the h1 and change its text
// 2. Select all .para elements and change their color to blue using a loop
// 3. Change the image's src and alt attributes
// 4. Create a CSS class "highlight" and toggle it on the first paragraph
// 5. Create 3 new <li> elements in JS and append them to #list
// 6. Remove the last paragraph from the page
```# Day-30
dom 1 DOM Selection &amp; Manipulation
