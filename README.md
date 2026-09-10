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

### Form submission

```html
<form id="myForm">
    <input id="nameInput" type="text">
    <button type="submit">Submit</button>
</form>
```

```js
const form = document.querySelector("#myForm");
const input = document.querySelector("#nameInput");

form.addEventListener("submit", (event) => {
    event.preventDefault();

    const name = input.value;

    console.log(name);
});
```

### Multiple inputs

```html
<form id="myForm">
    <input id="firstName" type="text">
    <input id="email" type="email">
    <button type="submit">Submit</button>
</form>
```

```js
form.addEventListener("submit", (event) => {
    event.preventDefault();

    const firstName = document.querySelector("#firstName").value;
    const email = document.querySelector("#email").value;

    console.log(firstName);
    console.log(email);
});
```

### Fetching an API

```js
const response = await fetch("https://api.example.com/data");
const data = await response.json();

console.log(data);
```

### Promises - .then() / .catch()

```js
fetch("https://api.example.com/data")
    .then(response => response.json())
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.error(error);
    });
```

### Promises - async / await

```js
async function getData() {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();

    console.log(data);
}

getData();
```

#### With try / catch

```js
async function getData() {
    try {
        const response = await fetch("https://api.example.com/data");
        const data = await response.json();

        console.log(data);
    }
    catch (error) {
        console.error(error);
    }
}
```

### Handling API response errors

```js
async function getData() {
    try {
        const response = await fetch("https://api.example.com/data");

        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        const data = await response.json();

        console.log(data);
    }
    catch (error) {
        console.error(error);
    }
}
```

### Parsing JSON

#### Convert response body into a JavaScript object

```js
const data = await response.json();

/*
{
    "name": "Pikachu",
    "type": "Electric"
}
*/
```

#### Access properties

```js
console.log(data.name);
console.log(data.type);
```

### JSON arrays

#### Access items

```js
/*
[
    {
        "name": "Pikachu"
    },
    {
        "name": "Charmander"
    }
]
*/

console.log(data[0].name);
console.log(data[1].name);
```

### Iterating through arrays

```js
const names = ["Pikachu", "Eevee", "Mew"];

names.forEach(name => {
    console.log(name);
});
```

#### Use .map() when you want to create a new array from an existing array.

```js
const names = ["Pikachu", "Eevee", "Mew"];

const upperNames = names.map(name => name.toUpperCase());

console.log(upperNames);
```

#### Mapping API data to HTML

```js
const html = data.map(pokemon => `
    <div class="card">
        <h2>${pokemon.name}</h2>
    </div>
`).join("");

container.innerHTML = html;
```

### Complete API example

```js
async function getPokemon() {
    try {
        const response = await fetch(
            "https://pokeapi.co/api/v2/pokemon"
        );

        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        const data = await response.json();

        const html = data.results.map(pokemon => `
            <div class="card">
                <h2>${pokemon.name}</h2>
            </div>
        `).join("");

        document.querySelector("#container").innerHTML = html;
    }
    catch (error) {
        console.error(error);
    }
}

getPokemon();
```

### CSS Grid

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}

/*
┌─────┐ ┌─────┐ ┌─────┐
│  1  │ │  2  │ │  3  │
└─────┘ └─────┘ └─────┘

┌─────┐ ┌─────┐ ┌─────┐
│  4  │ │  5  │ │  6  │
└─────┘ └─────┘ └─────┘
*/
```

### Responsive Grid

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}

@media (max-width: 768px) {
    .container {
        grid-template-columns: 1fr;
    }
}
```

### Automatic responsive columns

```css
.container {
    display: grid;
    grid-template-columns: repeat(
        auto-fit,
        minmax(250px, 1fr)
    );
    gap: 20px;
}
```
