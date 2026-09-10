# web-sba-cheatsheet

## DOM Manipulation & Card Styling

### Create an element

```js
const element = document.createElement("div");
```

### Add text

```js
const element = document.createElement("div");
```

### Add HTML

```js
element.innerHTML = "<strong>Hello World</strong>";
```

### Add a class

```js
element.classList.add("card");
```

### Append an element

```js
const container = document.querySelector("#container");

container.appendChild(element);
```

```js
container.append(element);
```

### Remove an element

```js
element.remove();
```

### Example - Create a card

```js
const card = document.createElement("div");

card.classList.add("card");
card.textContent = "My Card";

document.querySelector("#container").append(card);
```

### Accessing Elements by ID, Class & Tag

```js
const element = document.getElementById("myId");
const elements = document.getElementsByClassName("card");
const paragraphs = document.getElementsByTagName("p");

const element = document.querySelector("#myId");
const element = document.querySelector(".card");
const element = document.querySelector("p");
```

### Return all matching elements

```js
const cards = document.querySelectorAll(".card");
```

#### Can use:

```js
cards.forEach(card => {
    console.log(card);
});
```

### Event Listeners

```js
element.addEventListener("click", function () {
    console.log("Clicked!");
});

// Arrow function
element.addEventListener("click", () => {
    console.log("Clicked!");
});
```

### Common Events

"click"
"submit"
"input"
"change"
"mouseover"
"mouseout"
"keydown"
"keyup"

### Button Example

#### HTML

```html
<button id="myButton">Click Me</button>
```

#### JavaScript

```js
const button = document.querySelector("#myButton");

button.addEventListener("click", () => {
    console.log("Button clicked");
});
```

#### Event Object

```js
button.addEventListener("click", (event) => {
    console.log(event);
});
```

### Template Literals for HTML Generation

```js
const name = "Pikachu";

const html = `
    <div class="card">
        <h2>${name}</h2>
    </div>
`;

const pokemon = {
    name: "Pikachu",
    type: "Electric"
};

const html = `
    <div class="card">
        <h2>${pokemon.name}</h2>
        <p>Type: ${pokemon.type}</p>
    </div>
`;
```

### Array + Template Literals

```js
const cards = pokemonList.map(pokemon => `
    <div class="card">
        <h2>${pokemon.name}</h2>
    </div>
`).join("");

container.innerHTML = cards;
```

### JavaScript Styling

#### Inline

```js
element.style.color = "red";
element.style.backgroundColor = "blue";
element.style.fontSize = "20px";
```

#### CSS

```js
element.classList.add("error");

// Multiple classes
element.classList.add("card", "active");
```

```css
.error {
    background-color: red;
}
```

### Flexbox

#### Typical centered layout

```css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

#### Typical card layout

```css
.cards {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}
```

### Responsive card design

```html
<div class="cards">
    <div class="card">
        <h2>Card Title</h2>
        <p>Card content.</p>
    </div>
</div>
```

```css
.cards {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.card {
    flex: 1 1 250px;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 10px;
}
```

### Useful methods

```js
element.textContent
element.innerHTML
element.value
element.id
element.className
element.classList

element.append()
element.appendChild()
element.remove()
element.setAttribute()
element.getAttribute()
element.addEventListener()
element.querySelector()
element.querySelectorAll()
```

### Button generate HTML

```js
button.addEventListener("click", () => {
    output.innerHTML = `
        <div class="card">
            <h2>Hello</h2>
            <p>This was generated with JavaScript.</p>
        </div>
    `;
});
```

### Loop through elements

```js
const cards = document.querySelectorAll(".card");

cards.forEach(card => {
    card.addEventListener("click", () => {
        card.classList.toggle("active");
    });
});
```

```html
```

```html
```
