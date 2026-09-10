# DOM Manipulation

## Create an Element

```js
const element = document.createElement("div");
````

## Add Text

```js
element.textContent = "Hello World";
```

## Add HTML

```js
element.innerHTML = "<strong>Hello World</strong>";
```

## Add a Class

```js
element.classList.add("card");
```

Multiple classes:

```js
element.classList.add("card", "active");
```

Other class methods:

```js
element.classList.remove("card");
element.classList.toggle("active");
element.classList.contains("card");
```

## Append an Element

```js
const container = document.querySelector("#container");

container.append(element);
```

Or:

```js
container.appendChild(element);
```

## Remove an Element

```js
element.remove();
```

## Example: Create a Card

```js
const card = document.createElement("div");

card.classList.add("card");
card.textContent = "My Card";

document.querySelector("#container").append(card);
```

---

# Accessing Elements

## By ID

```js
const element = document.getElementById("myId");
```

## By Class

Returns a collection:

```js
const elements = document.getElementsByClassName("card");
```

## By Tag Name

Returns a collection:

```js
const paragraphs = document.getElementsByTagName("p");
```

## `querySelector()`

Returns the **first matching element**.

```js
const element = document.querySelector("#myId");
const element = document.querySelector(".card");
const element = document.querySelector("p");
```

Can use any CSS selector:

```js
document.querySelector(".card p");
document.querySelector("div.card");
```

## `querySelectorAll()`

Returns **all matching elements**:

```js
const cards = document.querySelectorAll(".card");
```

Can use:

```js
cards.forEach(card => {
    console.log(card);
});
```

---

# Event Listeners

## Basic Event Listener

```js
element.addEventListener("click", () => {
    console.log("Clicked!");
});
```

Or:

```js
element.addEventListener("click", function () {
    console.log("Clicked!");
});
```

## Common Events

```text
click
submit
input
change
mouseover
mouseout
keydown
keyup
```

## Button Example

### HTML

```html
<button id="myButton">Click Me</button>
```

### JavaScript

```js
const button = document.querySelector("#myButton");

button.addEventListener("click", () => {
    console.log("Button clicked");
});
```

## Event Object

```js
button.addEventListener("click", (event) => {
    console.log(event);
});
```

Useful properties:

```js
event.target
event.currentTarget
```

---

# Template Literals

Use **backticks** instead of quotation marks.

```js
const name = "Pikachu";

const html = `
    <div class="card">
        <h2>${name}</h2>
    </div>
`;
```

## Object Properties

```js
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

## Expressions

```js
const price = 10;
const quantity = 3;

const html = `
    <p>Total: $${price * quantity}</p>
`;
```

## Insert HTML

```js
container.innerHTML = html;
```

Or append to existing HTML:

```js
container.innerHTML += html;
```

## Array + Template Literals

```js
const cards = pokemonList.map(pokemon => `
    <div class="card">
        <h2>${pokemon.name}</h2>
    </div>
`).join("");

container.innerHTML = cards;
```

Remember:

```text
.map()   = creates a new array
.join()  = combines array into a string
```

---

# Forms & User Input

## Get Text from an Input

### HTML

```html
<input id="nameInput" type="text">
```

### JavaScript

```js
const input = document.querySelector("#nameInput");

const name = input.value;

console.log(name);
```

## Read Input as User Types

```js
input.addEventListener("input", () => {
    console.log(input.value);
});
```

## Form Submission

### HTML

```html
<form id="myForm">
    <input id="nameInput" type="text">
    <button type="submit">Submit</button>
</form>
```

### JavaScript

```js
const form = document.querySelector("#myForm");
const input = document.querySelector("#nameInput");

form.addEventListener("submit", (event) => {
    event.preventDefault();

    const name = input.value;

    console.log(name);
});
```

Important:

```js
event.preventDefault();
```

Stops the browser's default form submission.

## Multiple Inputs

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

## Clear an Input

```js
input.value = "";
```

## Set an Input Value

```js
input.value = "Hello";
```

## Check if Empty

```js
if (input.value.trim() === "") {
    console.log("Input is empty");
}
```

## Common Input Types

```html
<input type="text">
<input type="email">
<input type="password">
<input type="number">
<input type="checkbox">
<input type="radio">
```

Most inputs:

```js
input.value
```

Checkboxes:

```js
checkbox.checked
```

---

# API Fetching & Promises

## Basic `fetch()`

```js
const response = await fetch("https://api.example.com/data");
const data = await response.json();

console.log(data);
```

`fetch()` returns a **Promise**.

---

## `.then()` / `.catch()`

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

Typical flow:

```text
fetch()
   ↓
response.json()
   ↓
data
```

---

# Async / Await

Usually easier to read than `.then()` chains.

```js
async function getData() {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();

    console.log(data);
}

getData();
```

## With `try` / `catch`

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

---

# Handling API Response Errors

`fetch()` does **not** automatically throw an error for HTTP errors such as `404` or `500`.

Check `response.ok`:

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

Useful properties:

```js
response.ok
response.status
response.statusText
```

Common status codes:

```text
200 = OK
201 = Created
400 = Bad Request
401 = Unauthorized
403 = Forbidden
404 = Not Found
500 = Server Error
```

---

# Working with JSON

## Parse JSON

Convert the response body into a JavaScript object:

```js
const data = await response.json();
```

Example JSON:

```json
{
    "name": "Pikachu",
    "type": "Electric"
}
```

Access properties:

```js
console.log(data.name);
console.log(data.type);
```

---

# JSON Arrays

Example:

```json
[
    {
        "name": "Pikachu"
    },
    {
        "name": "Charmander"
    }
]
```

Access individual items:

```js
console.log(data[0].name);
console.log(data[1].name);
```

---

# Iterating Through Arrays

## `forEach()`

Use when you want to **perform an action for every item**.

```js
const names = ["Pikachu", "Eevee", "Mew"];

names.forEach(name => {
    console.log(name);
});
```

With index:

```js
names.forEach((name, index) => {
    console.log(index, name);
});
```

---

## `map()`

Use when you want to **create a new array** from an existing array.

```js
const names = ["Pikachu", "Eevee", "Mew"];

const upperNames = names.map(name => name.toUpperCase());

console.log(upperNames);
```

Result:

```text
["PIKACHU", "EEVEE", "MEW"]
```

## Mapping API Data to HTML

```js
const html = data.map(pokemon => `
    <div class="card">
        <h2>${pokemon.name}</h2>
    </div>
`).join("");

container.innerHTML = html;
```

Remember:

```text
forEach() = perform an action
map()     = create a new array
join()    = combine array into a string
```

---

# Complete API Example

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

---

# CSS Styling

## Inline Styling with JavaScript

```js
element.style.color = "red";
element.style.backgroundColor = "blue";
element.style.fontSize = "20px";
```

CSS property names use **camelCase** in JavaScript:

```text
background-color → backgroundColor
font-size        → fontSize
margin-top       → marginTop
```

## Prefer CSS Classes

JavaScript:

```js
element.classList.add("error");
```

CSS:

```css
.error {
    background-color: red;
}
```

---

# Flexbox

## Basic Flexbox

```css
.container {
    display: flex;
}
```

## Center Content

```css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

## Direction

```css
.container {
    flex-direction: row;
}
```

```css
.container {
    flex-direction: column;
}
```

Default:

```text
row
```

## `justify-content`

Controls the **main axis**.

```css
justify-content: flex-start;
justify-content: center;
justify-content: flex-end;
justify-content: space-between;
justify-content: space-around;
justify-content: space-evenly;
```

## `align-items`

Controls the **cross axis**.

```css
align-items: flex-start;
align-items: center;
align-items: flex-end;
align-items: stretch;
```

## Wrapping

```css
.container {
    display: flex;
    flex-wrap: wrap;
}
```

## Gap

```css
.container {
    gap: 20px;
}
```

## Typical Card Layout

```css
.cards {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}
```

## `flex`

```css
.card {
    flex: 1;
}
```

Responsive card sizing:

```css
.card {
    flex: 1 1 250px;
}
```

Equivalent to:

```text
flex-grow   flex-shrink   flex-basis
    1            1           250px
```

---

# CSS Grid

Grid is useful for **multi-column layouts**.

## Basic Grid

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}
```

Equivalent to:

```css
grid-template-columns: 1fr 1fr 1fr;
```

`1fr` = one fraction of the available space.

## Responsive Grid

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

## Automatic Responsive Columns

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

This automatically adjusts the number of columns based on available width.

## Spanning Columns

```css
.item {
    grid-column: span 2;
}
```

Spans 2 columns.

Specific columns:

```css
.item {
    grid-column: 1 / 3;
}
```

## Grid Rows

```css
.item {
    grid-row: span 2;
}
```

---

# Responsive Card Design

## HTML

```html
<div class="cards">
    <div class="card">
        <h2>Card Title</h2>
        <p>Card content.</p>
    </div>

    <div class="card">
        <h2>Another Card</h2>
        <p>More content.</p>
    </div>
</div>
```

## Flexbox Version

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

## Grid Version

```css
.cards {
    display: grid;
    grid-template-columns: repeat(
        auto-fit,
        minmax(250px, 1fr)
    );
    gap: 20px;
}

.card {
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 10px;
}
```

## Responsive Images

```css
.card img {
    width: 100%;
    height: auto;
}
```

## Media Query

```css
@media (max-width: 768px) {
    .cards {
        flex-direction: column;
    }
}
```

---

# CSS Selectors

## Element Selector

Selects all elements of that type:

```css
p {
    color: blue;
}
```

## Class Selector

```css
.card {
    padding: 20px;
}
```

HTML:

```html
<div class="card"></div>
```

## ID Selector

```css
#header {
    background-color: black;
}
```

HTML:

```html
<header id="header"></header>
```

## Descendant Selector

Selects elements inside another element:

```css
.card p {
    color: gray;
}
```

## Child Selector

Selects only **direct children**:

```css
.card > p {
    color: gray;
}
```

## Multiple Selectors

```css
h1, h2, h3 {
    font-family: sans-serif;
}
```

## Attribute Selector

```css
input[type="text"] {
    border: 1px solid black;
}
```

## Pseudo-Classes

```css
button:hover {
    background-color: gray;
}

button:active {
    transform: scale(0.98);
}

input:focus {
    outline: 2px solid blue;
}
```

Common pseudo-classes:

```text
:hover
:active
:focus
:checked
```

## Pseudo-Elements

```css
.card::before {
    content: "";
}

.card::after {
    content: "";
}
```

---

# CSS Specificity

Generally, higher specificity wins when rules conflict.

From lower → higher:

```text
Element       p
Class         .card
ID            #container
Inline        style=""
```

Example:

```css
p {
    color: blue;
}

.card p {
    color: green;
}

#main p {
    color: red;
}
```

Avoid using `!important` unless necessary.

---

# Useful DOM Properties & Methods

## Properties

```js
element.textContent
element.innerHTML
element.value
element.id
element.className
element.classList
```

## Methods

```js
element.append()
element.appendChild()
element.remove()

element.setAttribute()
element.getAttribute()

element.addEventListener()

element.querySelector()
element.querySelectorAll()
```

## DOM Traversal

```js
element.parentElement
element.children
element.firstElementChild
element.lastElementChild
element.nextElementSibling
element.previousElementSibling
```

---

# Common Patterns

## Button → Change Text

```js
const button = document.querySelector("#button");
const output = document.querySelector("#output");

button.addEventListener("click", () => {
    output.textContent = "Hello!";
});
```

## Button → Generate HTML

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

## Loop Through Elements

```js
const cards = document.querySelectorAll(".card");

cards.forEach(card => {
    card.addEventListener("click", () => {
        card.classList.toggle("active");
    });
});
```

## Form → Read Input

```js
form.addEventListener("submit", (event) => {
    event.preventDefault();

    const value = input.value;

    console.log(value);
});
```

## API → Display Data

```js
async function getData() {
    try {
        const response = await fetch("https://api.example.com/data");

        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        const data = await response.json();

        const html = data.map(item => `
            <div class="card">
                <h2>${item.name}</h2>
            </div>
        `).join("");

        document.querySelector("#container").innerHTML = html;
    }
    catch (error) {
        console.error(error);
    }
}

getData();
```

---

# Quick Reference

## JavaScript

```text
document.getElementById()
document.getElementsByClassName()
document.getElementsByTagName()

document.querySelector()
document.querySelectorAll()

document.createElement()

element.textContent
element.innerHTML
element.value

element.classList.add()
element.classList.remove()
element.classList.toggle()

element.append()
element.appendChild()
element.remove()

element.addEventListener()

event.target
event.preventDefault()
```

## Template Literals

```js
`Hello ${name}`
```

## Fetch

```js
const response = await fetch(url);
const data = await response.json();
```

## Error Handling

```js
if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
}
```

## Array Methods

```text
forEach() = perform an action for each item
map()     = create a new array
join()    = combine array into a string
```

## Flexbox

```css
display: flex;
flex-direction: row;
justify-content: center;
align-items: center;
flex-wrap: wrap;
gap: 20px;
flex: 1 1 250px;
```

## Grid

```css
display: grid;
grid-template-columns: repeat(3, 1fr);
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
gap: 20px;
```

## CSS Selectors

```css
p {}
.card {}
#header {}
.card p {}
.card > p {}
h1, h2 {}
input[type="text"] {}
button:hover {}
input:focus {}
.card::before {}
.card::after {}
```

# SBA Templates

## DOM Manipulation & Card Styling

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Template 1</title>
</head>

<body>
    <div class="card" id="book-card">
        <!-- Do not hardcode the content here, use JavaScript -->
    </div>

    <script>
        const book = {
            "id": 42,
            "title": "The Hitchhiker's Guide to the Galaxy",
            "author": "Douglas Adams",
            "year": 1979,
            "genres": ["Science Fiction", "Comedy", "Adventure"],
            "pages": 224,
            "language": "English",
            "imageUrl": "https://images-na.ssl-images-amazon.com/images/I/81XSN3hA5gL.jpg"
        };

        const card = document.getElementById("book-card");

        // Create elements
        const image = document.createElement("img");
        const content = document.createElement("div");
        const title = document.createElement("h1");
        const author = document.createElement("h2");
        const details = document.createElement("div");
        const year = document.createElement("p");
        const pages = document.createElement("p");
        const language = document.createElement("p");
        const genres = document.createElement("p");

        // Populate elements
        image.src = book.imageUrl;
        image.alt = book.title;

        title.textContent = book.title;
        author.textContent = book.author;

        year.textContent = `Year: ${book.year}`;
        pages.textContent = `Pages: ${book.pages}`;
        language.textContent = `Language: ${book.language}`;
        genres.textContent = `Genres: ${book.genres.join(", ")}`;

        // Build details section
        details.appendChild(year);
        details.appendChild(pages);
        details.appendChild(language);
        details.appendChild(genres);

        // Build content section
        content.appendChild(title);
        content.appendChild(author);
        content.appendChild(details);

        // Build card
        card.appendChild(image);
        card.appendChild(content);
    </script>

    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 40px;
        }

        .card {
            width: 300px;
            border: 1px solid #ccc;
            border-radius: 8px;
            background-color: white;
            color: #333;

            /* Flexbox */
            display: flex;
            flex-direction: column;

            overflow: hidden;
        }

        .card img {
            width: 100%;
            height: 300px;
            object-fit: cover;
        }

        .card > div {
            display: flex;
            flex-direction: column;
            padding: 15px;
            gap: 8px;
        }

        .card h1 {
            font-size: 1.5em;
            margin: 0;
        }

        .card h2 {
            margin: 0;
            font-size: 1em;
        }

        .card p {
            margin: 0;
        }

        .card h1,
        .card h2 {
            text-transform: uppercase;
        }
    </style>
</body>
</html>
```

## API Fetching & Multiple Cards

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Template 2</title>
</head>

<body>
    <div class="cards-container">
        <!-- Your cards will be added here using JavaScript -->
    </div>

    <script>
        const apiUrl = "https://reqres.in/api/users?per_page=12";

        async function loadUsers() {
            const container = document.querySelector(".cards-container");

            try {
                const response = await fetch(apiUrl);

                if (!response.ok) {
                    throw new Error(`HTTP error: ${response.status}`);
                }

                const data = await response.json();

                for (const user of data.data) {
                    const card = document.createElement("div");
                    const image = document.createElement("img");
                    const name = document.createElement("h2");
                    const email = document.createElement("p");

                    // Populate card
                    image.src = user.avatar;
                    image.alt = `${user.first_name} ${user.last_name}`;

                    name.textContent = `${user.first_name} ${user.last_name}`;
                    email.textContent = user.email;

                    // Add elements to card
                    card.appendChild(image);
                    card.appendChild(name);
                    card.appendChild(email);

                    // Add card to container
                    container.appendChild(card);
                }
            } catch (error) {
                console.error("Failed to fetch users:", error);
                container.textContent = "Failed to load users.";
            }
        }

        loadUsers();
    </script>

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 30px;
            background-color: #f4f4f4;
        }

        .cards-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            max-width: 1000px;
            margin: 0 auto;
        }

        .cards-container > div {
            display: flex;
            flex-direction: column;

            background-color: white;
            border: 1px solid #ccc;
            border-radius: 8px;
            overflow: hidden;

            /* Makes cards in the same row the same height */
            height: 100%;
        }

        .cards-container img {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }

        .cards-container h2,
        .cards-container p {
            margin: 10px 15px;
        }

        .cards-container p {
            margin-top: 0;
        }

        /* Stack cards on mobile */
        @media (max-width: 600px) {
            .cards-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</body>
</html>
```

## Filtering Data with Events

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Template 3</title>
</head>

<body>
    <div class="filter-container">
        <!-- Select will be added using JavaScript -->
    </div>

    <div class="cards-container">
        <!-- Cards will be added here using JavaScript -->
    </div>

    <script>
        const apiUrl = "https://jsonplaceholder.typicode.com/photos?_limit=20";

        let photos = [];

        const filterContainer = document.querySelector(".filter-container");
        const cardsContainer = document.querySelector(".cards-container");

        async function loadPhotos() {
            try {
                const response = await fetch(apiUrl);

                if (!response.ok) {
                    throw new Error(`HTTP error: ${response.status}`);
                }

                photos = await response.json();

                createFilter();
                displayCards(photos);
            } catch (error) {
                console.error("Failed to fetch photos:", error);
                cardsContainer.textContent = "Failed to load photos.";
            }
        }

        function createFilter() {
            const select = document.createElement("select");

            // "All" option
            const allOption = document.createElement("option");
            allOption.value = "all";
            allOption.textContent = "All Albums";
            select.appendChild(allOption);

            // Get unique album IDs
            const albumIds = [...new Set(photos.map(photo => photo.albumId))];

            // Create option for each album ID
            for (const albumId of albumIds) {
                const option = document.createElement("option");

                option.value = albumId;
                option.textContent = `Album ${albumId}`;

                select.appendChild(option);
            }

            // Listen for filter changes
            select.addEventListener("change", () => {
                const selectedAlbum = select.value;

                if (selectedAlbum === "all") {
                    displayCards(photos);
                } else {
                    const filteredPhotos = photos.filter(
                        photo => photo.albumId === Number(selectedAlbum)
                    );

                    displayCards(filteredPhotos);
                }
            });

            filterContainer.appendChild(select);
        }

        function displayCards(data) {
            // Clear existing cards
            cardsContainer.innerHTML = "";

            for (const photo of data) {
                const card = document.createElement("div");
                const image = document.createElement("img");
                const title = document.createElement("h2");
                const album = document.createElement("p");

                image.src = photo.thumbnailUrl;
                image.alt = photo.title;

                title.textContent = photo.title;
                album.textContent = `Album ID: ${photo.albumId}`;

                card.appendChild(image);
                card.appendChild(title);
                card.appendChild(album);

                cardsContainer.appendChild(card);
            }
        }

        loadPhotos();
    </script>

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 30px;
            background-color: #f4f4f4;
        }

        .filter-container {
            max-width: 1000px;
            margin: 0 auto 20px;
        }

        .filter-container select {
            padding: 8px;
            font-size: 1rem;
        }

        .cards-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            max-width: 1000px;
            margin: 0 auto;
        }

        .cards-container > div {
            display: flex;
            flex-direction: column;

            background-color: white;
            border: 1px solid #ccc;
            border-radius: 8px;
            overflow: hidden;

            height: 100%;
        }

        .cards-container img {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }

        .cards-container h2 {
            font-size: 1.1rem;
            margin: 15px 15px 5px;
        }

        .cards-container p {
            margin: 0 15px 15px;
        }

        @media (max-width: 600px) {
            .cards-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</body>
</html>
```
