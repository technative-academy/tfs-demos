# JavaScript Refresher

## Introducing JavaScript

JavaScript is a scripting language that you can use to define how your web page behaves.

- *HTML* is used for ***content***
- *CSS* is used for ***style***
- *JavaScript* is used for ***behaviour***


### Adding JavaScript to a web page

There are two ways to include a JavaScript in your web page:


#### Inline JavaScript

We won't be doing this ourselves but you may see examples where JavaScript is written *inline*, which means you write JavaScript within the HTML page:

```html
<script>
    // your JavaScript code goes here...
</script>
```


#### JavaScript files

Much like our CSS, we will be writing our JavaScript code in a separate file.

This is good practice as it makes sure that your JavaScript is separated from your content (HTML) and style (CSS) files.

Note that the difference between the previous example and the following example is the addition of the `defer` and `src` attributes, the latter of which references the name of the JavaScript file.

```html
<script defer src="filename.js"></script>
```

---

## Exercise - Adding JavaScript to HTML

Create a `time` folder, and within this create a new `html` file, a new `css` file and a new `js` file:

 - `time.css`
 - `time.html`
 - `time.js`

Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript</title>
        <link rel="stylesheet" href="time.css" />
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <script defer src="time.js"></script>
    </head>
    <body>
        <h1>JavaScript</h1>
        <p class="time">The current time will appear here!</p>
    </body>
</html>
```

And some CSS:

```css
.time {
    font-size: 48px;
    text-shadow: 2px 2px 2px green;
}

.orange {
    color: orange;
}
```

Open the HTML file in a web browser (e.g. Firefox).

Now open the JavaScript file `time.js` and enter the following code:

```js
alert("Hello world!");
```

Refresh the web page in your browser. Do you see an alert popup?

If that worked, now it's time to see how to programmatically generate some HTML content with JavaScript.


### The JavaScript console

Right-click in your browser and select "inspect element".

From the panel that pops up, look for the tab marked 'console'.

***Whenever you write JavaScript, make sure you remember to open the console!***

If you ever make a mistake when writing JavaScript, this is where an error gets displayed. It will show you the file name and line number where the mistake is located, along with a (sometimes cryptic) description of the error.

For now, remove what you added previously in your JavaScript file and replace it with the following:

```js
console.log("Attention, the universe!");
```

Refresh the page in the web browser.

The annoying alert popup should stop appearing, and you should see this message in the console instead.



### Updating HTML content with JavaScript

Now add the following to your JavaScript file:

```js
// calculate the current time
const timeNow = new Date().toUTCString();

// output the time to the console
console.log(timeNow);
```

Refresh the page in the web browser.

If you look in the browser console, do you now see the current time?

Refresh the page, and the time in the console should update.

Now to find out how to add the time to the HTML, add the following to the JavaScript file below what you have already:

```js
// find the HTML element in the page that has a class of "time"
const timeElement = document.querySelector(".time");

// update the content of the time HTML element with the current time
timeElement.textContent = timeNow;

// add an extra class to the time HTML element to change the text colour
timeElement.classList.add("orange");

```

Refresh the page. Does the current time appear in the page? Is it orange?

Don't worry for now what each line of code means, we'll cover this later. We're just demonstrating what is possible with JavaScript, something we can't do with just HTML and CSS.

If you get stuck, example files can be found here:

 - [time.html](examples/time/time.html)
 - [time.css](examples/time/time.css)
 - [time.js](examples/time/time.js)

---

## Exercise - Console

We're about to learn some JavaScript, and it will help to have somewhere to practice, so create a new HTML and JS file that we can experiment with:

* `console.html`
* `console.js`

Add the following HTML:

`console.html`:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Open the console!</title>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <script defer src="console.js"></script>
    </head>
    <body>
        <h1>Open the console!</h1>
        <p>Nothing to see here - try opening the console...</p>
    </body>
</html>
```

The JavaScript file will be empty for now, we'll add to it as we work through the next section.


---

## JavaScript Programming Concepts

In order to start using JavaScript, we need to cover a few programming concepts.


### Variables

*Variables* are one of the core concepts in programming.

We use them for storing and re-using information.

An analogy often used to describe a *variable* is that it is a container that you can put something in.

The name that you give a variable is the label you put on the container, so you know how to find it again later.

Variables can be used to store anything - numbers, text or other types of information:

```js
const nearestStar = "Alpha Centauri";
const lightYearsAway = 4.3;
const age = 6000000000;
const isHot = true;
```

When you need to reference that information later, refer to it via the variable name:

```js
console.log(nearestStar); // "Alpha Centauri"
```

Variables can be set using the values from other variables:

```js
const planets = 8;
const dwarfPlanets = 5;

const planetCount = planets + dwarfPlanets;
console.log(planetCount); // 13
```

The value of a variable can be changed (that's why it's called a *variable*):

```js
let numberOfPlanets = 9;

numberOfPlanets = numberOfPlanets - 1;
console.log(numberOfPlanets); // 8 - bye bye Pluto
```

### `const` and `let`

You may have noticed in the example above, we switched from using `const` to `let` when defining our variable.

If we are going to create a variable once and then never change its value, we can think of it as a *constant*, and so use the word `const` when creating it.

If we are going to change the value of the variable, we must use `let` instead.

If we try to update the value of a variable defined with `const`, we'll get an error (we'll learn about errors later).

If in doubt, we can create every variable as a `const`, then switch it to a `let` at a later date if we find that we need to change its value.

We may also see `var` used when creating variables - this is an older convention but still valid.

```js
// use 'const' when the variable value isn't going to change
const closestPlanetToTheSun = "Mercury";

// use 'let' when the variable value might change...
let planetCount = 8;

// ...then we can update it if we decide to make Pluto a planet again!
planetCount = planetCount + 1;

// or use 'var' which is also valid...
var furthestPlanetFromTheSun = "Pluto";

// ...this also means we can update its value
furthestPlanetFromTheSun = "Eris";
```


### Variable names

What you call the variable isn't important!

Variable names are case sensitive, and can't contain spaces or hyphens.

To use multiple words in a variable name, the convention is to `use_underscores_to_seperate` or `camelCaseVariableNames` (try to stick to one convention or the other, don't mix them)

```js
// camel-cased variable
const numberOfPlanets = 8;

// variable with underscores
const number_of_dwarf_planets = 5;
```

Be careful when re-using variable names, using the same name twice will overwrite the old value stored in the variable.


*Further reading:*

 - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar\_and\_types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types)

---


### Mathematical and logical operators

As you will have seen above, you use one equals sign `=` to **assign** a value to a variable:

```js
const planet = "Earth";
console.log(planet); // Earth
```


To concatenate values together (to combine multiple strings of text, such as in this next example) we use a `+`:

```js
const city = "London";
const country = "England";

const address = city + country;
console.log(address); // "LondonEngland"
```

Notice with the previous example that JavaScript doesn't automatically know that we should add a space between the two words, we'd need to do that manually, for example:

```js
const newAddress = city + ", " + country;
console.log(newAddress); // "London, England"
```

We can also manipulate numbers:

  - `+` can add two numbers together
  - `-` can subtract one number from another
  - `*` can multiply two numbers together
  - `/` can divide one number by another

```js
const firstNumber = 10;
const secondNumber = 2;

console.log(firstNumber + secondNumber); // 10 + 2 === 12
console.log(firstNumber - secondNumber); // 10 - 2 === 8
console.log(firstNumber * secondNumber); // 10 * 2 === 20
console.log(firstNumber / secondNumber); // 10 / 2 === 5
```

You can also compare values:

   - `===` checks if one value is equal to another
   - `!==` checks if one value is *not* equal to another
   - `>` checks if one value is greater than another
   - `>=` checks if one value is greater than or equal to another
   - `<` checks if one value is less than another
   - `<=` checks if one value is less than or equal to another

```js
const number = 10;

console.log(number === 1);  // false
console.log(number !== 1);  // true
console.log(number > 10);   // false
console.log(number >= 10);  // true
console.log(number < 10);   // false
console.log(number <= 10);  // true
```

---

### `if/else` conditionals, and program flow

`if/else` conditionals allow us to execute certain functionality only when specific conditions have been met.


#### `if`

As described above, you use three equals `===` signs to check if its value is **equal** to something else:

```js
// remember we set the value of planet earlier when we set:
// const planet = "Earth";

// Test the value of our variable
if (planet === "Earth") {
  console.log("We are on Earth, enjoy!");
}
```

You use `!==` to check if its value is **not equal** to something else:

```js
if (planet !== "Earth") {
  console.log("We are not on Earth, I hope you can hold your breath!");
}
```

**The code within the curly brackets `{…}` will only be processed if the condition between the brackets `(…)` is true.**

#### `else`

`else` can be used to specify code that should be processed if the condition between the brackets is false:

```js
if (planet === "Earth") {
    console.log("Enjoy the sunset");

} else {
    console.log("Beware the sunset!");
}
```

#### `else if`

`else if` can be used to specify multiple code blocks, one of which should be used:

```js
if (planet === "Earth") {
    console.log("Nice weather");

} else if (planet === "Mars") {
    console.log("Bit cold out");

} else if (planet === "Venus") {
    console.log("Bit hot out");

} else {
    console.log("Where am I?");
}
```

#### AND

If we want to check more than one condition, we can do so:

```js
const time = "1pm";

// do something if the planet is Earth AND it's lunch time
if (planet === "Earth" && time === "1pm") {
    console.log("Lunchtime on earth, falafel time!");

// it's either not Earth, or it isn't lunch time yet...
} else {
    console.log("I'm hungry...");
}
```


#### OR

If we want to check multiple possible values, we can do so:

```js
// do something if the planet is Mercury OR if the planet is Venus
if (planet === "Mercury" || planet === "Venus") {
    console.log("Take your coat off, it's hot out");

} else if (planet === "Earth") {
    console.log("Ah, just right");

} else {
    console.log("You might need an extra layer");
}

```

### if/else statement with numeric values

The examples above use if/else statements to test the text value of a variable.

We can also use if/else statements to check the numeric value of a variable:

```js
// set a variable (in millions of miles)
const distanceFromSun = 93;

if (distanceFromSun <= 90) {
    console.log("Bit hot out");

} else if (distanceFromSun > 90 &&  distanceFromSun <= 95) {
    console.log("Perfect weather");

} else {
    console.log("Bit cold out");
}
```


*Further reading:*

 - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)


---

## Exercise (continued)

If you get stuck, example files can be found here:

 - [console.html](examples/console/console.html)
 - [console.js](examples/console/console.js)

---

## Exercise

Create some new files:

 - `if-else.html`
 - `if-else.css`
 - `if-else.js`

Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript</title>
        <link rel="stylesheet" href="if-else.css" />
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <script defer src="if-else.js"></script>
    </head>
    <body>
        <h1>JavaScript</h1>
        <p class="time"></p>
    </body>
</html>
```

Add some CSS:

```css
.time {
    font-size: 48px;
    text-shadow: 2px 2px 2px green;
}
.orange {
    color: orange;
}
.green {
    color: green;
}
.blue {
    color: blue;
}
```

For the JavaScript file, we're going to use variables and an `if/else` statement to change the colour of the text according to the current time.

```js
// get the current time, but only the seconds
const seconds = new Date().getSeconds();
console.log(seconds);

// add the current time to the page
// (we'll discuss this properly later)
const timeElement = document.querySelector(".time");
timeElement.textContent = seconds;
```

Open this page in a browser, open the console, and check that the current number of seconds is displayed. When you refresh the page the number of seconds should update.

Now, write a JavaScript `if/else` condition that sets the colour of the text to orange, blue or green depending on how many seconds have passed in the current minute:

 - if the number of seconds is less than 20, set the text to *orange*
 - if the number of seconds is greater than 20 and less than 40, set the text to *green*
 - otherwise, set the text to *blue*

Here's an example of how you would change the text colour:

```js
timeElement.classList.add("orange");
```

If you get stuck, example files can be found here:

 - [if-else.html](examples/if-else/if-else.html)
 - [if-else.css](examples/if-else/if-else.css)
 - [if-else.js](examples/if-else/if-else.js)


---


### `for` loops

One of the reasons that we want to use JavaScript is to save us manually carrying out a repetitive task that could be automated.

`for` loops let us perform operations and execute commands multiple times.

They let us run a certain piece of code over and over again.

There are a few ways of creating a loop with JavaScript, but the most commonly used is this:

```js
for (let counter = 1; counter <= 10; counter++) {
    console.log(counter); //1, 2, 3, 4, ... 10!
}
```

The first line of the `for` loop statement has three parts, separated by semicolons:

- Part 1 (`let counter = 1`): we start with an initialisation of the variable `counter`. This will enable us to control how many times the loop is executed.

- Part 2 (`counter <= 10`): the second part is the test, or the stopping condition. The loop checks this statement every time it is run, and continues for as long as this is `true`

- Part 3 (`counter++`): This is an expression that is executed every time the loop runs. In this example we are increasing the value of `counter` by one.

These three steps lets us control the loop and manage when it should end, so that it doesn't go on forever.


---

## Exercise

Create some new files:

 - `for.html`
 - `for.css`
 - `for.js`

Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript</title>
        <link rel="stylesheet" href="for.css" />
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <script defer src="for.js"></script>
    </head>
    <body>
        <h1>I can count!</h1>
        <p class="time"></p>
    </body>
</html>
```

Add some CSS:

```css
.time {
    font-size: 48px;
    text-shadow: 2px 2px 2px green;
}
.orange {
    color: orange;
}
.green {
    color: green;
}
.blue {
    color: blue;
}
```

For the JavaScript file, we're going to write a `for` loop to add some numbers to the page.

At the start of your JavaScript file you want to add the following:

```js
// start the counter
// (we'll discuss this properly later)
const timeElement = document.querySelector(".time");
timeElement.textContent = "";
```

Below this, we want to add a `for` loop so that the page contains the numbers:

> _"1, 2, ... 10"_

This is the content that you would put within the `for` loop:

```js
timeElement.textContent = timeElement.textContent + counter + ", ";
```

If you get stuck, example files can be found here:

 - [for.html](examples/for/for.html)
 - [for.css](examples/for/for.css)
 - [for.js](examples/for/for.js)


---

## JavaScript tips

Later we'll continue to explore what we can do with JavaScript. For now, here are a few more tips that should help as you start to write it.

### Comments

Comments can be useful. JavaScript has two different types of comment:

  - Single-line comments which begin with two forward slashes (`//`) -  text to the right of these is ignored by the browser, until we start a new line:

  ```js
  // This is a single-line comment
  const planet = "Earth";
  ```

  - Multiline comments begin with `/*` and end with `*/`:

  ```js
  /*
     this is
     a multiline
     comment
  */
  const planet = "Earth";
  ```


### Errors

  - Errors with JavaScript are more common than with HTML/CSS.

  - A single error will stop all JavaScript on the page.

  - Remember to **always** have the console open when writing JavaScript in order to spot and fix errors.

---

## Functions

Functions are a set of instructions that can be specified (or defined) now, and then used (or called) later on.

So far we've been writing JavaScript code that is run immediately, as soon as the page loads.

But sometimes we only want the instructions we write in JavaScript to occur at certain times, for example only when the user clicks on a button.

That's what we'll be learning about next.

First, we need to know how to create a ***function***. This will let us prepare some code that we can use whenever we want.

After this, we'll learn how to use the function when someone interacts with our page in a specific way.

Another reason to use a function is that it lets us write code once and then you re-use it multiple times.

### Declaring a function

The first thing you need to do is *declare* a function:

```js
function enthuseAboutEarth() {
   console.log("I like the planet Earth");
}
```

### Calling a function

Once you've created your function, you can call it:

```js
enthuseAboutEarth(); // "I like the planet Earth"
```

In fact you can call it lots of times:

```js
enthuseAboutEarth(); // "I like the planet Earth"
enthuseAboutEarth(); // "I like the planet Earth"
enthuseAboutEarth(); // "I like the planet Earth"
```

Or even:

```js
for (let counter = 1; counter <= 10; counter++) {
    enthuseAboutEarth(); // "I like the planet Earth" x 10!
}
```

### Passing parameters to functions

This isn't a very useful function, it always does the same thing every time you call it.

To make it more useful, you can create a function that takes a *parameter*, so that you can reuse it with different values.

```js
function enthuse(planet) {
    console.log("I like the planet " + planet);
}
```

In this example, the `enthuse()` function takes one *parameter* (which here we have arbitrarily decided to call `planet`) and then it uses `console.log` to output some text using this parameter.

Now you can call this function multiple times, passing in a different parameter to receive a different sentence:

```js
enthuse("Mercury"); // "I like the planet Mercury"
enthuse("Earth");   // "I like the planet Earth"
```

If you want to pass more than one parameters, separate them with commas:

```js
function addColourToPlanet(planetSelector, planetName, colour) {
    …
}
```

And when you call the function, again use commas:

```js
addColourToPlanet(".mercury", "Mercury", "orange");
```

We'll see some examples of this shortly.

### Returning a value from a function

The examples above use `console.log` to output to the console when you call a function. This is useful for demonstrating how a function works, but it isn't very useful when you want the function to do something.

Instead, we usually use functions to ***return*** something that we can then use, for example:

```js
function enthuse(planet) {
    return "I like the planet " + planet;
}

const sentenceAboutEarth = enthuse("Earth");
console.log(sentenceAboutEarth); // "I like the planet Earth"

const sentenceAboutMars = enthuse("Mars");
console.log(sentenceAboutMars); // "I like the planet Mars"
```

This will be useful in future examples.


---

## Exercise

Create new `html`, `css` and `js` files:

 - `function.html`
 - `function.css`
 - `function.js`

Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript function</title>
        <link rel="stylesheet" href="function.css">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <script defer src="function.js"></script>
    </head>
    <body>
        <h1>Open the console...</h1>
    </body>
</html>
```

Add some CSS:

```css
p {
    font-size: 48px;
    margin-bottom: 24px;
    text-shadow: 2px 2px 2px green;
}
```

Open the HTML file in a web browser (e.g. Firefox).

Don't forget to open the JavaScript console too.

Now open the JavaScript file `function.js` and enter the following code:

```js
function enthuse(planet) {
    return "I like the planet " + planet;
}

const mercurySentence = enthuse("Mercury");
console.log(mercurySentence);

const earthSentence = enthuse("Earth");
console.log(earthSentence);
```

Refresh the web page in your browser, and open the console.

Do you see the two sentences? If not, are there any errors in the JavaScript console?

Now in the web browser's JavaScript console, try adding sentence for the planet Saturn.

Try creating a new function (with a different name), one that takes two parameters and uses them to construct another sentence. Call this function twice, passing it different parameters each time, and log the results in the console.

If you get stuck, example files can be found here:

 - [function.html](examples/function/function.html)
 - [function.css](examples/function/function.css)
 - [function.js](examples/function/function.js)

---

## Manipulating HTML with JavaScript

JavaScript functions are useful, but the examples we've seen so far wouldn't help for a typical website - most people don't browse the web with the console open.

To make JavaScript useful, we want to use it to update our HTML page.

We had an example of this earlier, but at the time we didn't spend much time looking at how we were doing this.


### Selecting HTML elements with JavaScript

Before we can use JavaScript to change our HTML, we first need to select the HTML element that we want to manipulate.

We can do this with the function `document.querySelector();`

This is an example of a *native* or 'built-in' JavaScript function, something that web browsers already understand.

If we had this HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript example</title>
        <script defer src="example.js"></script>
    </head>
    <body>
        <h1>…</h1>
        <p class="sentence">…</p>
    </body>
</html>
```

If we wanted to select the HTML element `<p class="sentence">…</p>` we would write this in our JavaScript file:

```js
const sentenceElement = document.querySelector(".sentence");
```

The *parameter* we pass to this function - `".sentence"` - is the same as the CSS selector we would write to refer to this HTML element. We add a dot at the start because we're selecting via its `class` attribute, exactly as we do with CSS.

Alternatively if we wanted to select the `<h1>…</h1>` element we could add this to our JavaScript:

```js
const h1Element = document.querySelector("h1");
```

Note that we haven't added a dot at the start because we're selecting an element - again, exactly as you would with CSS.

Once we have selected the HTML element, we can manipulate it.

*(Just a reminder, what we call the variables above isn't important!)*


### Updating HTML text content with JavaScript

If we want to change the text contained within the HTML element, we would set its `textContent` value.

For example, to update the text of the two elements we have selected above we would write:

```js
h1Element.textContent = "This is the title";
sentenceElement.textContent = "This is the sentence";
```

This will update our HTML so that the page would now look like this in a browser:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript</title>
        <script defer src="example.js"></script>
    </head>
    <body>
        <h1>This is the title</h1>
        <p class="sentence">This is the sentence</p>
    </body>
</html>
```

We can change the text to anything, including a variable. Remember that function we created earlier? Here's an example of how we could use it:

```js
// declare the function
function enthuse(planet) {
    return "I like the planet " + planet;
}

// now call the function to create a sentence
const mercurySentence = enthuse("Mercury"); // "I like the planet Mercury"

// and then add that sentence to the page
const sentenceElement = document.querySelector(".sentence");
sentenceElement.textContent = mercurySentence;
```

This would update our HTML to be:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript example</title>
        <script defer src="example.js"></script>
    </head>
    <body>
        <h1>This is the title</h1>
        <p class="sentence">I like the planet Mercury</p>
    </body>
</html>
```


---

## Exercise

Let's manipulate some HTML with JavaScript.

Create some new files:

 - `sentence.html`
 - `sentence.css`
 - `sentence.js`

Here's the HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="sentence.css" />
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <script defer src="sentence.js"></script>
    </head>
    <body>
        <h1>Planets of the solar system</h1>
        <p class="mercury"></p>
        <p class="venus"></p>
        <p class="earth"></p>
    </body>
</html>
```

Here's the CSS:

```css
p {
    font-size: 48px;
    margin-bottom: 24px;
    text-shadow: 2px 2px 2px green;
}
```

For the JavaScript, we want to select each of the three planet HTML elements and add some text:

```js
function createPlanetSentence(planetName) {
    console.log("You have called createPlanetSentence() with the following parameters");
    console.log(planetName);

    // this is where you need to create a sentence about the planet!
}

// call the function to style each planet
const mercurySentence = createPlanetSentence("Mercury");
const venusSentence = createPlanetSentence("Venus");
// create a similar variable for Earth!

// this is where you add the code to add these three sentences to the page!

```

We want to add one line of JavaScript *inside* our `createPlanetSentence` function. Remember that we are passed the variable `planetName`:

   ```js
return "I quite like the planet " + planetName;
   ```

Once we have our sentence, we need to add it to the page.

1. Select the HTML element using `document.querySelector()` and update the HTML element's text content:

  ```js
  const mercuryElement = document.querySelector(".mercury");
  mercuryElement.textContent = mercurySentence;
  ```

2. Now do the same for Venus and Earth!

The end goal is to make the JavaScript dynamically update your HTML to this (you don't need to manually update your HTML, this is just an example):

```html
<p class="mercury">I quite like the planet Mercury</p>
<p class="venus">I quite like the planet Venus</p>
<p class="earth">I quite like the planet Earth</p>
```

If you get stuck, example files can be found here:

 - [sentence.html](examples/sentence/sentence.html)
 - [sentence.css](examples/sentence/sentence.css)
 - [sentence.js](examples/sentence/sentence.js)

---


## Updating HTML `class` attribute with JavaScript

As well as updating the content of the HTML element, we can also add (or remove) a `class` on the HTML element.

This is a useful way to change the styles of an HTML element.

If we had the HTML we saw earlier:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript example</title>
        <script defer src="example.js"></script>
    </head>
    <body>
        <h1>This is the title</h1>
        <p class="sentence">I like the planet Mercury</p>
    </body>
</html>
```

If we also had the JavaScript we saw earlier to select the sentence element:

```js
// find the sentence element
const sentenceElement = document.querySelector(".sentence");
```

To update the `class` attribute of this HTML element you use the following function:

```js
sentenceElement.classList.add("orange");
```

This would add the `class` of `orange` to that HTML element, so it would change the HTML to:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript example</title>
        <script defer src="example.js"></script>
    </head>
    <body>
        <h1>This is the title</h1>
        <p class="sentence orange">I like the planet Mercury</p>
    </body>
</html>
```

And to remove a `class`:

```js
sentenceElement.classList.remove("orange");
```

---

## Exercise

Let's expand on the last exercise, this time let's use a function with multiple parameters.

Create some new files:

 - `functions.html`
 - `functions.css`
 - `functions.js`

Here's the HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="functions.css" />
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <script defer src="functions.js"></script>
    </head>
    <body>
        <h1>Planets of the solar system</h1>
        <p class="mercury"></p>
        <p class="venus"></p>
        <p class="earth"></p>
    </body>
</html>
```

And the CSS:

```css
p {
    font-size: 48px;
    margin-bottom: 24px;
    text-shadow: 2px 2px 2px green;
}

.orange {
    color: orange;
}
.green {
    color: green;
}
.blue {
    color: blue;
}
```

For the JavaScript, we want to select each of the three planet HTML elements, add some text and colour each one:

```js
function addColourToPlanet(planetSelector, planetName, colour) {
    console.log("You have called addColourToPlanet() with the following parameters");
    console.log(planetSelector, planetName, colour);

    // this is where you need to write your JavaScript!
}

// call the function to style Mercury
addColourToPlanet(".mercury", "Mercury", "orange");

// call the function to style Venus
addColourToPlanet(".venus", "Venus", "green");

// call the function to style Earth
addColourToPlanet(".earth", "Earth", "blue");
```

We want to add three lines inside our JavaScript function:

1. Select the HTML element using `document.querySelector()` and the supplied variable `planetSelector`:

  ```js
  const planetElement = document.querySelector(planetSelector);
  ```

2. Update the HTML element's text content using the supplied variable `planetName`:

  ```js
  planetElement.textContent = planetName;
  ```

3. Add a `class` to the HTML element using the supplied variable `colour`:

  ```js
  planetElement.classList.add(colour);
  ```

This will make your HTML update to this (you don't need to manually update your HTML, this is just an example):

```html
<p class="mercury orange">Mercury</p>
<p class="venus green">Venus</p>
<p class="earth blue">Earth</p>
```

If you get stuck, example files can be found here:

 - [functions.html](examples/functions/functions.html)
 - [functions.css](examples/functions/functions.css)
 - [functions.js](examples/functions/functions.js)

---

## HTML forms

We now know how to create functions, and how to manipulate our HTML with JavaScript.

At the moment we're still running this code as soon as the web page loads. Instead, we want to learn how to only run our code when a user interacts with our page. To learn how to do that, we need to learn about *forms*.

We want to be able to capture information from a user. The main way to do this is by using HTML form elements.

You will be familiar with using these, as they are used frequently on many websites:

 - text inputs
 - radio buttons
 - checkboxes
 - select (dropdown) lists
 - buttons
 - (etc)

These form elements are useful because JavaScript can be used both to read information from them, and write information to them.

_(Note that in some of the following examples we also use a `<label>` element to add text next to each input.)_


### Text inputs

HTML:

```html
<input type="text" name="planet-name" placeholder="Placeholder text" />

<textarea name="planet-description" placeholder="About the planet" rows="5" cols="50"></textarea>
```

Which creates:

>
> <input type="text" name="planet-name" placeholder="Placeholder text" />
>
> <textarea name="planet-description" placeholder="About the planet" rows="5" cols="50"></textarea>
>

### Radio buttons

HTML:

```html
<label>
    <input type="radio" name="planet-type" value="Rocky" />
    Rocky
</label>

<label>
    <input type="radio" name="planet-type" value="Gas giant" />
    Gas giant
</label>
```

Which creates:

>
> <label>
>    <input type="radio" name="planet-type" value="Rocky" />
>    Rocky
> </label>
>
> <label>
>    <input type="radio" name="planet-type" value="Gas giant" />
>    Gas giant
> </label>
>


### Checkboxes

HTML:

```html
<label>
    <input type="checkbox" name="planet-atmosphere" value="Oxygen" />
    Oxygen
</label>

<label>
    <input type="checkbox" name="planet-atmosphere" value="Nitrogen" />
    Nitrogen
</label>
```

Which creates:

>
> <label>
>    <input type="checkbox" name="planet-atmosphere" value="Oxygen" />
>    Oxygen
> </label>
>
> <label>
>    <input type="checkbox" name="planet-atmosphere" value="Nitrogen" />
>    Nitrogen
> </label>
>

### Select

HTML:

```html
<label>
    Favourite planet
    <select name="planet-favourite">
        <option></option>
        <option>Mercury</option>
        <option>Venus</option>
        <option>Earth</option>
        <option>Mars</option>
    </select>
</label>
```

Which creates:

>
> <label>
    Favourite planet
    <select name="planet-favourite">
        <option></option>
        <option>Mercury</option>
        <option>Venus</option>
        <option>Earth</option>
        <option>Mars</option>
    </select>
</label>
>


### Buttons

HTML:

```html
<button>Submit form</button>
```

Which creates:

>
> <button>Submit form</button>

---


## Events

Note that with the form elements above, although the browser displays these form elements and we can interact with them, they don’t actually *do* anything. We need to write some JavaScript to respond to users interacting with them.

The main way to do this is to detect an *event*, such as a user clicking on a button or entering text.

An event can be thought of in the following way:

> _When 'this' happens, do 'that'_

An example:

> _When a user clicks on a button, display some text_


### Adding an event listener

We listen for events with the JavaScript function `addEventListener()`

There are different events that we can listen for with JavaScript. Some common events are:

 * `keypress`: When a user presses a key on their keyboard
 * `click`: When a user clicks on the element
 * `mouseover`: When the mouse pointer moves over an element

Here's an example of how you might listen for a `click` event on an HTML `<button>` element:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>JavaScript event example</title>
        <link rel="stylesheet" href="example.css" />
        <script defer src="example.js"></script>
    </head>
    <body>
        <p class="button-text">No clicks detected yet</p>
        <button class="button-toggle">Click me</button>
    </body>
</html>
```

And the JavaScript:

```js
// we're going to count how many times the button has been clicked
let clickCount = 0;

// call this function every time the button is clicked
function updateParagraphText() {

    // increase the click count
    clickCount = clickCount + 1;

    // update the text
    const paragraphElement = document.querySelector(".button-text");
    paragraphElement.textContent = "The button has been clicked " + clickCount + " times";
}

// select the button
const buttonElement = document.querySelector(".button-toggle");

// add the click event listener to call our function
buttonElement.addEventListener("click", updateParagraphText);
```

You can see it in action here:

>
> <p class="button-text">No clicks detected yet</p>
> <button class="button-toggle">Click me</button>
>

<script>
let clickCount = 0;

function updateParagraphText() {
    clickCount = clickCount + 1;

    const pElement = document.querySelector(".button-text");
    pElement.textContent = "The button has been clicked " + clickCount + " times";
}

const buttonElement = document.querySelector(".button-toggle");
buttonElement.addEventListener("click", updateParagraphText);
</script>

---

## Exercise

Time to add some interactive form elements to a web page. We're going to create a web page with some buttons that change elements on the page.

Create some new files:

 - `events.html`
 - `events.css`
 - `events.js`

Here's the HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="events.css" />
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <script defer src="events.js"></script>
    </head>
    <body>
        <h1>What's your favourite planet?</h1>
        <button class="mercury">Mercury</button>
        <button class="venus">Venus</button>
        <button class="earth">Earth</button>
        <p class="result">(No planet selected yet)</p>
        <p>(I have changed my mind <span class="click-count">0</span> times)</p>
    </body>
</html>
```

And the CSS:

```css
p {
    font-size: 48px;
    margin-bottom: 24px;
    text-shadow: 2px 2px 2px green;
}

.orange {
    color: orange;
}
.green {
    color: green;
}
.blue {
    color: blue;
}
```

For the JavaScript, we want to do a few things:

 - Select each of the three buttons, here's an exmaple of selecting the first one:

  ```js
  const mercuryButton = document.querySelector(".mercury");
  ```

 - Add an event listener to each of the buttons, again here's an example for the first one

  ```js
  mercuryButton.addEventListener("click", selectMercury);
  ```

 - When a button is clicked, we call a function to update the `textContent` of `<p class="result"></p>` with the name of the selected planet

 ```js
    function selectMercury() {
        const resultElement = document.querySelector(".result");
        resultElement.textContent = "Mercury";
    }
 ```

Try creating similar functionality for the other two planets.

Once you have this working, you could go further:

 - Create a variable to keep track of how many times any button has been clicked

  ```js
  let clickCounter = 0;
  ```

 - When a button is clicked, increment the value of this variable

 ```js
 // add this to the end of the selectMercury() function
 clickCounter = clickCounter + 1;
 ```

 - Use the value of this variable to update the `textContent` of `<span class="click-count"></span>`

 ```js
 // add this to the end of the selectMercury() function
 const clickElement = document.querySelector(".click-count");
 clickElement.textContent = clickCounter;
 ```


If you get stuck, example files can be found here:

 - [events.html](examples/events/events.html)
 - [events.css](examples/events/events.css)
 - [events.js](examples/events/events.js)

Here's an updated version of the JavaScript file, removing some of the code repetition - the end result is the same but it's a bit shorter to write, although more complicated to understand - see if you can follow the logic:

 - [events-revised.js](examples/events/events-revised.js)


---


## Iterating through collections

The JavaScript example above allows us to update our HTML with JavaScript, but it's not very efficient.

We need to manually tell the JavaScript to find and update each individual HTML element.

If we were to add a new element to our HTML - let's say we wanted to add Mars - we would need to manually update our JavaScript too.

There is a better way to select *every* element on the page that matches a selector, and carry out the same operation on it.

We can achieve this by using a 'collection' of HTML elements.

> _(The technical name for this collection is an *array* - we'll learn more about them later)._


### Selecting multiple elements

The example in the recap above selects **one** element on the page that matches a selector.

It does this using the JavaScript function `querySelector()`

Instead, we want to select **every** element on the page that matches a selector.

We can do this using the JavaScript function `querySelectorAll()`

If we have the following HTML:

```html
<ul>
    <li class="planet">Mercury</li>
    <li class="planet">Venus</li>
    <li class="planet">Earth</li>
    <li class="planet">Mars</li>
</ul>
```

We could select **all** of the elements with a class of `planet` using the following JavaScript:

```js
const planetElements = document.querySelectorAll(".planet");
```

This creates a variable called `planetElements` which is a *collection* (or *array*) of HTML elements that have a `class` of `"planet"`  in the HTML page.


### `foreach` loops

We can now do something with this collection - we can run a function for each of the four HTML elements that were found in our example HTML above.

We will use `forEach` to do this - something we first learnt about earlier:

```js
// this is what we want to do to each planet element
function updatePlanet(planetElement) {
    planetElement.classList.add("blue");
}

// this is how we loop through each of the planet elements
planetElements.forEach(updatePlanet);
```

The example below calls the function `updatePlanet` for each element in the `planetElements` collection.

The first time it will pass in the first HTML element, so `planetElement` will be `<li class="planet">Mercury</li>`

The next time it will pass in the second HTML element (Venus), and so on, until it has run once for each HTML element in the `planetElements` collection.

Each time it runs, the class of `"blue"` will be added to the HTML element.

This is what it will do to the HTML in the browser:

```html
<ul class="planets">
    <li class="planet blue">Mercury</li>
    <li class="planet blue">Venus</li>
    <li class="planet blue">Earth</li>
    <li class="planet blue">Mars</li>
</ul>
```

Using `document.querySelectorAll` and a `foreach` loop is a useful way to automatically update our web pages, as we'll see later.

---

### `for` loops

There is an alternative way to achieve the same solution but it's perhaps not so easy to understand.

It's using a `for` loop as we saw earlier.


```js
// this is what we want to do to each planet element
function updatePlanet(planetElement) {
    planetElement.classList.add("blue");
}

// this is how we loop through each of the planet elements
for (let counter = 0; counter < planetElements.length; counter++) {
    const planetElement = planetElements[counter];
    updatePlanet(planetElement);
}
```

We mentioned how important `for` loops are when we want to perform the same task many times. Here is a case where we want to do the same thing to each element.

The example above runs the code between the opening and closing curly bracket `{...}` for each element in the collection.

Each time, we select the current element in the loop by referencing `planetElements[counter]` - remember that in a `for` loop, the value of `counter` is incremented each time the code loops.

We generally use `foreach` loops when possible as they're often a bit more straightforward than a `for` loop.

---

## Exercise

We're going to test the code above.

Create new `html`, `css` and `js` files:

 - `foreach.html`
 - `foreach.js`
 - `foreach.css`

Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="foreach.css" />
        <script defer src="foreach.js"></script>
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <ul class="planets">
            <li class="planet">Mercury</li>
            <li class="planet">Venus</li>
            <li class="planet">Earth</li>
            <li class="planet">Mars</li>
            <li class="planet">Jupiter</li>
            <li class="planet">Saturn</li>
            <li class="planet">Uranus</li>
            <li class="planet">Neptune</li>
        </ul>
    </body>
</html>
```

And some CSS:

```css
.planet {
    font-size: 24px;
    margin-bottom: 12px;
    text-shadow: 2px 2px 2px green;
}

.orange {
    color: orange;
}

.green {
    color: green;
}

.blue {
    color: blue;
}

button {
    margin: 5px;
    padding: 10px;
}

.currently-selected-button {
    background: black;
    color: orange;
}

.planet-details {
    display: none;
    margin: 5px;
    padding: 10px;
    font-size: 24px;
    margin-bottom: 12px;
    text-shadow: 2px 2px 2px green;
}

.currently-selected-planet {
    display: block;
}

.log {

}
```

Open the HTML file in a web browser (e.g. Firefox).

Remember to open the JavaScript console so that you can spot any errors.

Now open the JavaScript file `foreach.js` and enter the following code:

```js
// retrieve all planet elements
const planetElements = document.querySelectorAll(".planet");

// use this function to add the class to each planet
function updatePlanet(planetElement) {
    planetElement.classList.add("blue");
}

// loop through the planet elements
planetElements.forEach(updatePlanet);
```

Refresh the web page in your browser. Has the text changed colour?

If so, try changing the colour from `blue` to `orange`.

Refresh the page, has it worked?

Try updating the HTML - add Pluto as a (dwarf) planet. You should see that you don't need to change the JavaScript at all, but it will also now work for this element too.

If you get stuck, example files can be found here:

 - [foreach.html](examples/foreach/foreach.html)
 - [foreach.js](examples/foreach/foreach.js)
 - [foreach.css](examples/foreach/foreach.css)


---


### Adding event listeners to collections

Earlier we saw an example of adding event listeners to several buttons.

If you look at the JavaScript file for that example, you'll see that we repeated ourselves several times.

Now that we know how to loop through a collection of elements on the page, we can also use the same technique to add event listeners to multiple elements.

This means we can *significantly* reduce the amount of code we wrote earlier.

It has the added advantage that if we were to add new HTML buttons, they would work automatically without needing to change the JavaScript.

The example below shows how you can add listeners to lots of buttons so that we know when certain buttons have been clicked.

If we had the following HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <script defer src="example.js"></script>
        <link rel="stylesheet" href="example.css" />
    </head>
    <body>

        <button class="planet-button">Mercury</button>
        <button class="planet-button">Venus</button>
        <button class="planet-button">Earth</button>

    </body>
</html>
```

We could loop through and add the same listener to each button:

```js
// find all button elements
const planetButtonElements = document.querySelectorAll(".planet-button");

// loop through all button elements
planetButtonElements.forEach(addPlanetButtonListener);

// add an event listener to each button element
function addPlanetButtonListener(planetButtonElement) {
    planetButtonElement.addEventListener("click", planetButtonClick);
}

// when a button is clicked, this is what we want to happen
function planetButtonClick() {
    alert("A button has been clicked!");
}
```

That would give us the following:

>
> <button class="planet-button-1">Mercury</button>
> <button class="planet-button-1">Venus</button>
> <button class="planet-button-1">Earth</button>
>

<script>
const planetButtonElements1 = document.querySelectorAll(".planet-button-1");
planetButtonElements1.forEach(addPlanetButtonListener1);

function addPlanetButtonListener1(planetButtonElement1) {
    planetButtonElement1.addEventListener("click", planetButtonClick1);
}

function planetButtonClick1() {
    alert("A button has been clicked!");
}
</script>

This is a good start, but it would be more helpful if we could identify which of the buttons had been clicked.

To do this, we can add an extra parameter (or *variable*) to the `planetButtonClick` function, one that is automatically created by the click event. It can be called anything, but we'll call it `event`:

```js
// when a button is clicked, this is what we want to happen
function planetButtonClick(event) {
    const clickedButton = event.currentTarget;
    alert("You clicked " + clickedButton.textContent);
}
```

That would give us the following:

>
> <button class="planet-button-2">Mercury</button>
> <button class="planet-button-2">Venus</button>
> <button class="planet-button-2">Earth</button>
>

<script>
const planetButtonElements2 = document.querySelectorAll(".planet-button-2");
planetButtonElements2.forEach(addPlanetButtonListener2);

function addPlanetButtonListener2(planetButtonElement2) {
    planetButtonElement2.addEventListener("click", planetButtonClick2);
}

function planetButtonClick2(event) {
    const clickedButton = event.currentTarget;
    alert("You clicked " + clickedButton.textContent);
}
</script>

Now that we know which button has been clicked, we can update our web page to display which option someone has clicked.

---

## Exercise

We're going to test the code above, to display a list of options, and show which one the user selects.

Create new `html` and `js` files:

 - `event-listeners.html`
 - `event-listeners.css`
 - `event-listeners.js`


Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>What is your favourite planet?</title>
        <script defer src="event-listeners.js"></script>
        <link rel="stylesheet" href="event-listeners.css" />
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <h1>What is your favourite planet?</h1>
        <div class="planet-buttons">
            <button class="planet-button">Mercury</button>
            <button class="planet-button">Venus</button>
            <button class="planet-button">Earth</button>
            <button class="planet-button">Mars</button>
            <button class="planet-button">Jupiter</button>
            <button class="planet-button">Saturn</button>
            <button class="planet-button">Uranus</button>
            <button class="planet-button">Neptune</button>
        </div>
        <p class="result"></p>
    </body>
</html>
```

And the CSS:

```css
.planet {
    font-size: 24px;
    margin-bottom: 12px;
    text-shadow: 2px 2px 2px green;
}

.orange {
    color: orange;
}

.green {
    color: green;
}

.blue {
    color: blue;
}

button {
    margin: 5px;
    padding: 10px;
}

.currently-selected-button {
    background: black;
    color: orange;
}

.planet-details {
    display: none;
    margin: 5px;
    padding: 10px;
    font-size: 24px;
    margin-bottom: 12px;
    text-shadow: 2px 2px 2px green;
}

.currently-selected-planet {
    display: block;
}

.log {

}
```

Open the HTML file in a web browser (e.g. Firefox).

Remember to open the console so that you can spot any errors.

Now open the JavaScript file `event-listeners.js` and enter the following code:

```js
// find all button elements
const planetButtonElements = document.querySelectorAll(".planet-button");

// loop through all button elements
planetButtonElements.forEach(addPlanetButtonListener);

// add an event listener to each button element
function addPlanetButtonListener(planetButtonElement) {
    planetButtonElement.addEventListener("click", planetButtonClick);
}

// on click, do something with the selected button
function planetButtonClick(event) {
    // find the HTML element that was clicked
    const clickedButton = event.currentTarget;

    // for now, just alert the answer
    // (you'll change this line in a minute!)
    alert("You clicked " + clickedButton.textContent);
}
```

Refresh the web page in your browser.

Click a button. Do you see an alert with the name of the planet?

Once you have this working, there are two further additions we can make to this JavaScript to make it useful.


### Displaying the text of the selected button

First, we can display the text from the selected button in the page, rather than in an alert (which becomes annoying very quickly).

In order to do so, we need to use the `document.querySelector()` function to select the HTML `<p class="result></p>` element that we have already added to the HTML page. We are going to store a reference to this HTML element in a variable called `resultElement`.

We can then use `resultElement.textContent` to set the value of this HTML element to the text content of the selected button.

We want this logic to run when someone clicks the button, so we add it to the `planetButtonClick` function.

```js
// on click, do something with the selected button
function planetButtonClick(event) {
    // find the HTML element that was clicked
    const clickedButton = event.currentTarget;

    // replace the 'alert' with the code below, to update the page

    // update the result
    const resultElement = document.querySelector(".result");
    resultElement.textContent = "You selected " + clickedButton.textContent;
}
```

Try this and see if it works.


### Updating the class of the selected button

As well as updating the text of the result element, we can also update the `class` of the selected button to indicate that it has been clicked:

```js
// on click, do something with the selected button
function planetButtonClick(event) {
    // find the HTML element that was clicked
    const clickedButton = event.currentTarget;

    // update the result
    const resultElement = document.querySelector(".result");
    resultElement.textContent = "You selected " + clickedButton.textContent;

    // add the selected state just to button that was clicked
    clickedButton.classList.add("currently-selected-button");
}
```

Try it in a browser and see how it works.

Click a few buttons.

Do you see a problem?


### Updating the class of the buttons that *haven't* been selected

The above example works, but it doesn't automatically deselect buttons that have been clicked in the past.

To do this, when a button has been clicked we first need to loop through all buttons and remove any prior clicked state *before* we then set the clicked state on the selected button:

```js
// on click, do something with the selected button
function planetButtonClick(event) {
    // find the HTML element that was clicked
    const clickedButton = event.currentTarget;

    // update the result
    const resultElement = document.querySelector(".result");
    resultElement.textContent = "You selected " + clickedButton.textContent;

    // remove selected state from all buttons
    planetButtonElements.forEach(updateClickedButtonState);

    // add selected state just to the clicked button
    clickedButton.classList.add("currently-selected-button");
}

// remove the currently selected state for all buttons
function updateClickedButtonState(planetButtonElement) {
    planetButtonElement.classList.remove("currently-selected-button");
}
```

Note that we need to remove the old class *before* we add it to the button that has just been clicked - if we tried to remove the clicked state afterwards we'd be adding the class and then immediately removing it again.


If you get stuck, example files can be found here:

 - [event-listeners.html](examples/event-listeners/event-listeners.html)
 - [event-listeners.css](examples/event-listeners/event-listeners.css)
 - [event-listeners.js](examples/event-listeners/event-listeners.js)

---

## Exercise

The example above demonstrates how you can update the text of an HTML element based on the click of a button.

This example could be extended further to show or hide an entire block of content based on the selected button.

Create new `html` and `js` files:

 - `text.html`
 - `text.css`
 - `text.js`

Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="text.css" />
        <script defer src="text.js"></script>
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <h1>Click on a planet to see a fact!</h1>
        <div class="planet-buttons">
            <button class="planet-button">Mercury</button>
            <button class="planet-button">Venus</button>
            <button class="planet-button">Earth</button>
        </div>

        <div class="planet-details planet-details-Mercury">
            Mercury is the closest planet to the Sun
        </div>

        <div class="planet-details planet-details-Venus">
            A day is longer than a year on Venus
        </div>

        <div class="planet-details planet-details-Earth">
            Earth has life!
        </div>
    </body>
</html>
```

And the CSS:

```css
.planet {
    font-size: 24px;
    margin-bottom: 12px;
    text-shadow: 2px 2px 2px green;
}

.orange {
    color: orange;
}

.green {
    color: green;
}

.blue {
    color: blue;
}

button {
    margin: 5px;
    padding: 10px;
}

.currently-selected-button {
    background: black;
    color: orange;
}

.planet-details {
    display: none;
    margin: 5px;
    padding: 10px;
    font-size: 24px;
    margin-bottom: 12px;
    text-shadow: 2px 2px 2px green;
}

.currently-selected-planet {
    display: block;
}

.log {

}
```

Open the HTML page in a web browser.

You should see that the three `<div class="planet-details"></div>` blocks have been hidden with CSS when the page loads.

Now we want to write some JavaScript that detects a click on each button.

When a button is clicked, we want to select the corresponding detail block and display it, hiding the others.

The JavaScript will look similar to what we have written previously:

```js
// find all planet buttons
const planetButtonElements = document.querySelectorAll(".planet-button");
planetButtonElements.forEach(addPlanetButtonListener);

// add an event listener for each button
function addPlanetButtonListener(planetButtonElement) {
    planetButtonElement.addEventListener("click", planetButtonClick);
}

// when a button has been clicked, show its content
function planetButtonClick(event) {
    const clickedButton = event.currentTarget;

    // the rest of the code will go here...
}
```

First, we want to generate the class of the selected planet's details element.

For example, if the user clicks on the 'Venus' button we want to select the HTML element with the class `planet-details-Venus`:

```js
// generate the class of the selected planet's details element
// for example: ".planet-details-Venus" or ".planet-details-Earth"
const detailsElementCssSelector = ".planet-details-" + clickedButton.textContent;
```

We then want to find the HTML element with this `class`:

```js
// find this element
const detailsElement = document.querySelector(detailsElementCssSelector);
```

Like in the previous example, we want to remove the selected state from all other detail elements before we display this one:

```js
// remove selected state from all details elements
const planetDetailElements = document.querySelectorAll(".planet-details");
planetDetailElements.forEach(updatePlanetDetailState);
```

Finally, we can display the selected detail element:

```js
// add selected state just to the clicked button
detailsElement.classList.add("currently-selected-planet");
```

Don't forget you'll need to create the `updatePlanetDetailState` function too:

```js
function updatePlanetDetailState(planetDetailElement) {
    planetDetailElement.classList.remove("currently-selected-planet");
}
```

Refresh the page, has it worked?

If you get it working, try adding extras:

 - Add a class to the selected button too, so the user can easily see which planet has been selected each time
 - Add images into each of the HTML blocks.
 - Add a new button and new content for Mars.

If you get stuck, example files can be found here:

 - [text.html](examples/text/text.html)
 - [text.css](examples/text/text.css)
 - [text.js](examples/text/text.js)


### Tabs!

We now know how to create tabbed content.

Here's an example page, you'll see the JavaScript is *exactly* the same as for the exercise above, only the HTML and CSS has changed.

 - [tabs.html](examples/tabs/tabs.html)
 - [tabs.css](examples/tabs/tabs.css)
 - [tabs.js](examples/tabs/tabs.js)

---

## Creating new HTML elements with JavaScript

So far we have been using JavaScript to update the HTML of our web page.

JavaScript can also be used to create new HTML elements and add them to the page. We'll see why this is useful later when we look at importing data from external sources into our web pages.

For now we'll see an example of creating new elements to keep a log of events that have taken place in our page.


### Creating a new HTML element

To create a new HTML element we can use the function `document.createElement()`

This function takes a single *parameter*, the type of element to create, such as `"p"`, `"li"` or `"h1"`:

```js
const newListElement = document.createElement("li");
```

With this line of code we have created a new element, but it is currently empty.

We can add both text content and a `class` using functions we've already been using:

```js
newListElement.classList.add("log-item");
newListElement.textContent = "New log item";
```

Our new element would now look like this:

```html
<li class="log-item">New Log item</li>
```

However, it wouldn't be visible yet as we haven't added it to our HTML page. To do that we need to know where in the page we would like it to exist. For example if we had the following HTML:

```html
<p>Here is a log of everything we've done so far:</p>
<ul class="log"></ul>
```

We would want to add our new list items to the `<ul "log"></ul>` element.

First, we need to select this:

```js
const logElement = document.querySelector(".log");
```

Then, we can add our new list item using the function `document.appendChild()`:

```js
logElement.appendChild(newListElement);
```

The completed JavaScript would look like this:

```js
const newListElement = document.createElement("li");
newListElement.classList.add("log-item");
newListElement.textContent = "New log item";

const logElement = document.querySelector(".log");
logElement.appendChild(newListElement);
```
---

## Exercise

Let's extend what we created for the previous exercise and add a log to display

Create two new files:

 - `log.html`
 - `log.css`
 - `log.js`

Copy the HTML and JS that you wrote in the last exercise, and paste it into these files.

Don't forget when you paste the HTML, you will need to change the name of the JavaScript file you are using.

You need to update:

```html
<script defer src="text.js"></script>
```

to:

```html
<script defer src="log.js"></script>
```

Next, add this to the HTML page at the bottom - **before** the closing `</body>` tag:

```html
<p>Here is a log of everything we've done so far</p>
<ul class="log"></ul>
```

Add this to the end of the JavaScript:

```js
function updateLog(planetName) {
    // get the current time
    const timeNow = new Date().toUTCString();

    // create a new element
    const newListElement = document.createElement("li");

    // add a class to the new element
    newListElement.classList.add("log-item");

    // add the text content to the new element
    newListElement.textContent = timeNow + ": " + planetName + " clicked";

    // add the new element to the HTML
    const logElement = document.querySelector(".log");
    logElement.appendChild(newListElement);
}
```

You may recognise the `timeNow` line from the examples we worked on earlier.

This function will add a new item to the log every time it is called.

We now need to add a call to this function every time a button is clicked, so add this to the bottom of the `planetButtonClick` function:

```js
// update the log
updateLog(clickedButton.textContent);
```


If you get stuck, example files can be found here:

 - [log.html](examples/log/log.html)
 - [log.css](examples/log/log.css)
 - [log.js](examples/log/log.js)


---

## Structured data with JavaScript objects and arrays

We have learnt about JavaScript variables, which are useful for storing bits of information that we may use again later:

```js
const planet = "Mercury";
const secondPlanet = "Venus";
const planet3 = "Earth";
...
const planetEight = "Neptune";
```
We have learnt how to do something with these variables, such as display their content in an HTML page.

For example, if we had the following empty element in our HTML page:

```html
<ul class="planets"></ul>
```
To add a list of planet names into the HTML element above we write the following JavaScript:

```js
// first, create a function to add each planet name to the page
function addPlanetToPage(planetName) {
    // create a new element
    const planetElement = document.createElement("li");
    planetElement.textContent = planetName;

    // add the new element to the page
    const planetListElement = document.querySelector(".planets");
    planetListElement.appendChild(planetElement);
}

// then, call this function for each planet
addPlanetToPage(planet);
addPlanetToPage(anotherPlanet);
addPlanetToPage(planet3);
...
addPlanetToPage(planetEight);
```

This would generate the following HTML:

```html
<ul class="planets">
    <li>Mercury</li>
    <li>Venus</li>
    <li>Earth</li>
    ...
    <li>Neptune</li>
</ul>
```

Luckily there are only eight planets in the solar system and so we'd only need to call this function eight times. But this is an inefficient way to handle information, to have to generate every single one manually. Imagine if there were hundreds of planets.

There is a better way!

---


## Arrays

We can store related pieces of information in an *array*.

This allows us to group information together, and later to run code for each individual piece of data in the array.

With reference to the example above, we could store the name of each planet in a single array:

```js
const planets = [
    'Mercury',
    'Venus',
    'Earth',
    'Mars',
    'Jupiter',
    'Saturn',
    'Nepture',
    'Uranus',
];
```

Now that we have the information in a single array, we can do clever things with it.

We can calculate how many values we have - how many planets there are:

```js
console.log(planets.length); // 8
```

Each item within an array can be thought of as a variable.

These individual array items are accessed by following the array’s variable name with an *index* enclosed in square brackets.

So, to access an individual item in the array we use the following code:

```js
const firstPlanet = planets[0]; // "Mercury"
const thirdPlanet = planets[2]; // "Earth"
```

Note that the *index* starts from _0_, so the first value - "Mercury" - is `planets[0]` and "Earth" would be `planets[2]` (not 3) and so on. ([This is why](https://dev.to/cerchie/why-do-computers-count-from-zero-3mh6))

We can use a `forEach()` *loop* to carry out an operation on every individual item in the array.

In the example below we re-use the function we saw earlier, which will add a planet name to the page:

```js
function addPlanetToPage(planetName) {
    // create a new element
    const planetElement = document.createElement("li");
    planetElement.textContent = planetName;

    // add the new element to the page
    const planetListElement = document.querySelector(".planets");
    planetListElement.appendChild(planetElement);
}
```

To call this function for every item in the array we can now use a `forEach` loop:

```js
planets.forEach(addPlanetToPage);
```

That's it!

If we wanted to add another planet, we would just add it to the array. Then it would automatically get added to the page.

This technique is most useful when we're dealing with data that we don't create ourselves, such as when we gather information from an external source and display it on a web page. We won't know what the content of the data is, but we will have an idea of its structure. When we receive this data, as long as we know its structure we can manipulate it. We'll see an example of this later.

---

## Exercise

Create new `html`, `css` and `js` files:

 - `arrays.html`
 - `arrays.js`
 - `arrays.css`

Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="arrays.css">
        <script defer src="arrays.js"></script>
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <p>There are <span class="planet-count"></span> planets</p>
        <ul class="planets"></ul>
    </body>
</html>
```

And some CSS:

```css
.planet {
  border: 2px solid black;
  border-radius: 50%;
  height: 250px;
  width: 250px;
  padding: 10px;
  margin: 20px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

p {
  margin: 0;
}

.planet-name {
  font-weight: bold;
  font-size: 24px;
}

.planet-circumference,
.planet-distance {
  font-style: italic;
}

.planet-Earth {
  background: green;
}

.planet-Mars {
  background: red;
}

.search {
  padding: 10px;
  font-size: 16px;
}

.hide {
  display: none;
}
```

Open the HTML file in a web browser (e.g. Firefox).

Remember to open the console so that you can spot any errors.

Now open the JavaScript file `arrays.js` and enter the following code:

```js
// create our data
const planets = [
    'Mercury',
    'Venus',
    'Earth',
    'Mars',
    'Jupiter',
    'Saturn',
    'Nepture',
    'Uranus',
];

// create the function to add the planet to the page
function addPlanetToPage(planetName) {
    // create a new element
    const planetElement = document.createElement("li");
    planetElement.textContent = planetName;

    // add the new element to the page
    const planetListElement = document.querySelector(".planets");
    planetListElement.appendChild(planetElement);
}

// add all planets
planets.forEach(addPlanetToPage);
```

Refresh the web page in your browser. Have the planets appeared?

To add styles to each planet, we need to add a `class` to each planet element. Add the third line below after the first two that you already have:

```js
// (THESE TWO LINES ALREADY EXIST)
const planetElement = document.createElement("li");
planetElement.textContent = planetName;

// (ADD THIS LINE BEFORE THE END OF THE FUNCTION)
planetElement.classList.add("planet");
```

Refresh in the browser, do the planets look different now?

To add the planet count value to the empty `span` element, add this code to the bottom of the JavaScript file:

```js
const planetCountElement = document.querySelector(".planet-count");
planetCountElement.textContent = planets.length;
```

Try adding Pluto to the end of the array. Refresh the page and see how the list and the count changes.

If you get stuck, example files can be found here:

 - [arrays.html](examples/arrays/arrays.html)
 - [arrays.css](examples/arrays/arrays.css)
 - [arrays.js](examples/arrays/arrays.js)


---

## Objects

Arrays are useful for allowing us to loop through a collection of items. We have just seen how we can use it to print the name of each planet.

The problem with the array example above is that we can't use it to store and display structured information about each planet. What if we wanted to do more than just display the name of each planet?

For example, we might want to print a few details about each planet, such as its circumference and distance from the sun.

If we want to store detailed information, we can use an *object*:

```js
const planet = {
    name: "Earth",
    circumference: "40,000 km",
    distanceFromSun: "150,000,000 km",
};
```

Note that objects uses curly brackets `{}`, where arrays use square brackets `[]`.

Values in an object can be accessed in two different ways - either way is fine, you'll see both used when you look at examples online:

```js
planet.name    // "Earth"
planet["name"] // "Earth"

planet.distanceFromSun     // "150,000,000 km"
planet["distanceFromSun"]  // "150,000,000 km"
```

---

## Exercise

We're going to display structured information about a planet - Earth.

Create new `html` and `js` files:

 - `objects.html`
 - `objects.css`
 - `objects.js`

Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="objects.css" />
        <script defer src="objects.js"></script>
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <h1>Planets of the solar system</h1>
        <div class="planets"></div>
    </body>
</html>
```

Add some CSS:

```css
.planet {
  border: 2px solid black;
  border-radius: 50%;
  height: 250px;
  width: 250px;
  padding: 10px;
  margin: 20px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

p {
  margin: 0;
}

.planet-name {
  font-weight: bold;
  font-size: 24px;
}

.planet-circumference,
.planet-distance {
  font-style: italic;
}

.planet-Earth {
  background: green;
}

.planet-Mars {
  background: red;
}

.search {
  padding: 10px;
  font-size: 16px;
}

.hide {
  display: none;
}
```

Open the HTML page in a web browser. Don't forget to open the console.

Now we want to write some JavaScript that creates details about the Earth.

Open up the JavaScript file. The first thing we want to add is information about the planet:

```js
const earth = {
    name: "Earth",
    circumference: "40,000 km",
    distanceFromSun: "150,000,000 km",
};
```

Now that we have some data, we need to add information about it to the page. Add the following code underneath the data you just added:

```js
function addPlanetToPage(planet) {
    // create a div element for the planet
    const planetElement = document.createElement("div");
    planetElement.classList.add("planet");
    planetElement.classList.add("planet-" + planet.name);

    // add the planet name
    const planetName = document.createElement("p");
    planetName.classList.add("planet-name");
    planetName.textContent = planet.name;
    planetElement.appendChild(planetName);

    // add the planet to the page
    const planetListElement = document.querySelector(".planets");
    planetListElement.appendChild(planetElement);
}

// add the planet to the page
addPlanetToPage(earth);
```

Refresh the page, has it worked? If not, look in the browser console to see if there are any errors.

Now that we have the planet name appearing, we also want to add the details about the planet.

For example, to add the circumference data beneath the planet name, add the following code inside the `addPlanetToPage` function:

```js
    // add other planet details
    const planetCircumference = document.createElement("p");
    planetCircumference.classList.add("planet-circumference");
    planetCircumference.textContent = "Circumference: " + planet.circumference;
    planetElement.appendChild(planetCircumference);
```

Note that it's important where you add this code. It should be added after you've added the planet name (line 11 in the example above).

Once you have this working, try to also add the planet's distance from the sun to the page.

If you get stuck, example files can be found here:

 - [objects.html](examples/objects/objects.html)
 - [objects.css](examples/objects/objects.css)
 - [objects.js](examples/objects/objects.js)


---

## Structured data

The real benefit of all this comes when you combine *objects* and *arrays* to create structured data.

For example, if we wanted to store information about every planet in the solar system we could structure it like this:

```js
const planets = [
    {
        name: "Mercury",
        circumference: "2,500 km",
        distanceFromSun: "57,000,000 km",
    },
    {
        name: "Venus",
        circumference: "28,000 km",
        distanceFromSun: "108,000,000 km",
    },
    {
        name: "Earth",
        circumference: "40,000 km",
        distanceFromSun: "150,000,000 km",
    }
];
```

We have already seen how we can select an individual item from the array, for example to select Earth we would use the following code:

```js
const earth = planets[2];
```

Once we have this variable, we can access details about Earth:

```js
earth.distanceFromSun // "150,000,000 km"
```

If we wanted to create a sentence that displayed how far Earth was from the sun, we could extract it from our data using the following code:

```js
const earth = planets[2];
console.log(earth.name + " is " + earth.distanceFromSun + " away from the sun");
```

Alternatively we could loop through each planet in the array and output this sentence for each of them:

```js
function displayPlanetData(planet) {
    console.log(planet.name + " is " + planet.distanceFromSun + " away from the sun");
}

planets.forEach(displayPlanetData);
// Mercury is 57,000,000 km away from the sun
// Venus is 108,000,000 km away from the sun
// Earth is 150,000,000 km away from the sun
```

---

## Exercise

We're going to display structured information about the planets.

Create new `html` and `js` files:

 - `structured.html`
 - `structured.css`
 - `structured.js`

Add some HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="structured.css" />
        <script defer src="structured.js"></script>
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <h1>Planets of the solar system</h1>
        <div class="planets"></div>
    </body>
</html>
```

And some CSS:

```css
.planet {
  border: 2px solid black;
  border-radius: 50%;
  height: 250px;
  width: 250px;
  padding: 10px;
  margin: 20px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

p {
  margin: 0;
}

.planet-name {
  font-weight: bold;
  font-size: 24px;
}

.planet-circumference,
.planet-distance {
  font-style: italic;
}

.planet-Earth {
  background: green;
}

.planet-Mars {
  background: red;
}

.search {
  padding: 10px;
  font-size: 16px;
}

.hide {
  display: none;
}
```

Open the HTML page in a web browser. Don't forget to open the console.

Now we want to write some JavaScript that creates details about each planet.

Open up the JavaScript file. The first thing we want to add is information about each planet:

```js
const planets = [
    {
        name: "Mercury",
        circumference: "2,500 km",
        distanceFromSun: "57,000,000 km",
    },
    {
        name: "Venus",
        circumference: "28,000 km",
        distanceFromSun: "108,000,000 km",
    },
    {
        name: "Earth",
        circumference: "40,000 km",
        distanceFromSun: "150,000,000 km",
    }
];
```

Now that we have some data, we need to loop through it to add information about each planet to the page.

We can use the **same** JavaScript function that we used in the previous example. In your new JS file, copy across the `addPlanetToPage()` function that you wrote, or copy the following:

```js
function addPlanetToPage(planet) {
    // create a div element for each element
    const planetElement = document.createElement("div");
    planetElement.classList.add("planet");
    planetElement.classList.add("planet-" + planet.name);

    // add the planet name
    const planetName = document.createElement("p");
    planetName.classList.add("planet-name");
    planetName.textContent = planet.name;
    planetElement.appendChild(planetName);

    // add other planet details
    const planetCircumference = document.createElement("p");
    planetCircumference.classList.add("planet-circumference");
    planetCircumference.textContent = "Circumference: " + planet.circumference;
    planetElement.appendChild(planetCircumference);

    const planetDistance = document.createElement("p");
    planetDistance.classList.add("planet-distance");
    planetDistance.textContent = "Distance from sun: " + planet.distanceFromSun;
    planetElement.appendChild(planetDistance);

    // add the planet to the page
    const planetListElement = document.querySelector(".planets");
    planetListElement.appendChild(planetElement);
}
```

The only difference now is how we call this function. Rather than calling it manually for each planet, we can loop through every planet object in the `planets` array automatically by adding this to the end of the file:

```js
planets.forEach(addPlanetToPage);
```

Refresh the page, has it worked? If not, look in the browser console to see if there are any errors.


### Additional tasks

 - Earth is green, the other planets don't currently have a background colour. See if you can work out how to add some CSS styles to colour the other planets. Maybe change their sizes too.

 - Try adding Mars (distance 227,000,000km, circumference 21,000km)

If you get stuck, example files can be found here:

 - [structured.html](examples/structured/structured.html)
 - [structured.css](examples/structured/structured.css)
 - [structured.js](examples/structured/structured.js)


---

## Filtering content

So far we have looped through our structured information and displayed everything that we had in the data.

Before we display this information, we can filter it. This allows us to dynamically display data only if it meets certain conditions.

This next example combines several things that we've learnt so far in the module.

---

## Exercise

We're going to show and hide our structured information about the planets, depending on what search term someone enters into a form input.

Create new `html` and `js` files:

 - `filter.html`
 - `filter.css`
 - `filter.js`

First, duplicate the HTML and JavaScript from the previous exercise. Note that in the HTML file you need to update the references to the JS file to point to these new file you've just created (e.g. change `structured.js` to `filter.js`).

These are the updates we then need to make:


### HTML

We need to add an HTML form with a text input field. When someone adds text, we will only display planet information if the name of the planet matches the text that has been entered.

We start with adding a text input field to the HTML page, put this above the `<div class="planets"></div>` element:

```html
<label>
    Search planets:
    <input type="text" name="search" class="search" placeholder="Enter words to search for" />
</label>
```

### JavaScript

Now we need to update the JavaScript.

First, let's add data for all of the planets rather than just the three/four we were working with before:

```js
const planets = [
    {
        name: "Mercury",
        circumference: "2,500 km",
        distanceFromSun: "57,000,000 km",
    },
    {
        name: "Venus",
        circumference: "28,000 km",
        distanceFromSun: "108,000,000 km",
    },
    {
        name: "Earth",
        circumference: "40,000 km",
        distanceFromSun: "150,000,000 km",
    },
    {
        name: "Mars",
        circumference: "227,000,000km",
        distanceFromSun: "21,000km",
    },
    {
        name: "Jupiter",
        circumference: "779,000,000km",
        distanceFromSun: "440,000km",
    },
    {
        name: "Saturn",
        circumference: "1,430,000,000km",
        distanceFromSun: "365,000km",
    },
    {
        name: "Uranus",
        circumference: "2,880,000,000km",
        distanceFromSun: "160,000km",
    },
    {
        name: "Neptune",
        circumference: "4,500,000,000km",
        distanceFromSun: "154,000km",
    }
];
```

The following code should sit below the code you copied over from the previous example.

First we add JavaScript to 'listen' for text being entered into the HTML form we just created:

```js
// listen to changes in the search form
const searchInput = document.querySelector(".search");
searchInput.addEventListener("input", updateSearchValue);

// initial search value, which will be empty
let searchValue = "";

// check what search term has been entered
function updateSearchValue() {
    // trim() removes any spaces before/after the input
    // toLowerCase() makes the entered text lowercase
    searchValue = searchInput.value.trim().toLowerCase();

    console.log("You searched for: " + searchValue);

    // you will add some more code here shortly...
}
```

This will set the value of the variable `searchValue` to whatever text has been entered into the form.

Now we need to update each of the planet elements when this text changes.

Add the following inside the `updateSearchValue()` function:

```js
    // loop through all planet elements
    // show or hide each one based on the search term
    const planetElements = document.querySelectorAll(".planet");
    planetElements.forEach(showOrHidePlanet);
```

Now we need to create this function that will show or hide each planet:

```js
// every time the text field changes, run this
function showOrHidePlanet(planetElement) {
    // you will add some code here shortly
}
```

First we want to check if a search term has been added. If no search term has been added we should show every planet.

Add this into the `showOrHidePlanet()` function:

```js
    // if no search value is set, show the planet
    if (searchValue.length === 0) {
        planetElement.classList.remove("hide");
    } else {
        // you will add code here shortly
    }
```

If a search term *has* been added, we want to filter and only show planets if the names match.

Note that the first few lines here are what we just entered - we're adding the `else` statement here to filter based on planet names.

```js
    // if no search value is set, show the planet
    if (searchValue.length === 0) {
        planetElement.classList.remove("hide");

    // if a search term has been set,
    // only display the planet if its name matches the search term
    } else {

        // get the name of the planet from its planet-name element
        const planetName = planetElement.querySelector(".planet-name").textContent.toLowerCase();
        if (planetName.includes(searchValue)) {
            planetElement.classList.remove("hide");
        } else {
            planetElement.classList.add("hide");
        }
    }
```

If you get stuck, example files can be found here:

 - [filter.html](examples/filter/filter.html)
 - [filter.css](examples/filter/filter.css)
 - [filter.js](examples/filter/filter.js)


---


## External data

We have learnt how to create structured data in JavaScript:

```js
const planets = [
    {
        name: "Mercury",
        circumference: "2,500 km",
        distanceFromSun: "57,000,000 km"
    },
    {
        name: "Venus",
        circumference: "28,000 km",
        distanceFromSun: "108,000,000 km"
    }
];
```

We then used the data above to populate a web page. This is the JavaScript that we wrote in order to do this:

```js
// add each planet to the page
planets.forEach(addPlanetToPage);

// function called for each planet in the loop
function addPlanetToPage(planet) {
    // create a div element for each element
    const planetElement = document.createElement("div");
    planetElement.classList.add("planet");
    planetElement.classList.add("planet-" + planet.name);

    // add the planet name
    const planetName = document.createElement("p");
    planetName.classList.add("planet-name");
    planetName.textContent = planet.name;
    planetElement.appendChild(planetName);

    // add the planet to the page
    const planetListElement = document.querySelector(".planets");
    planetListElement.appendChild(planetElement);
}
```

---

## Loading external data with `fetch`

With the example above, we didn't separate the information that we're going to display from the logic that actually displays it. If you look at the JavaScript file, the two blocks of code are together in the same file.

We can create a modified version of this where the data is stored separately from the logic. We can then use a JavaScript function called `fetch` in order to import the data so that we can access and manipulate it.

There are many advantages in separating our content from our logic, as we'll see shortly.


### Storing data as JSON

In order to do this, the first thing we need to do is create our data file. To do this we need to make a small modification to the content above - we'll be storing our data in **JavaScript Object Notation** *(JSON)* format.

The main difference from before is that all text will need to be surrounded by double-quotes:

```json
[
    {
        "name": "Mercury",
        "circumference": "2,500 km",
        "distanceFromSun": "57,000,000 km"
    },
    {
        "name": "Venus",
        "circumference": "28,000 km",
        "distanceFromSun": "108,000,000 km"
    }
]
```

We also need to be careful that we don't put a comma (`,`) at the end of the last piece of information - we could do it with JavaScript, but we can't in JSON.

We can't use comments (`//` or `/* ... */`) either.

We need to make sure our JSON is *valid*, which means it doesn't contain any errors. If the JSON does contain an error it won't work as expected. We can test it by copying and pasting our JSON into an online website like [jsonlint.com](https://jsonlint.com/) and clicking "Validate JSON".

Once we know our JSON is valid, to load it into our JavaScript we need to use the JavaScript `fetch` function:

```js
fetch('our-data-file.json')
    .then((response) => response.json())
    .then((data) => {
        console.log('Data: ', data);

        // at this point we can do something with our JSON data
        // it is available in the variable "data"
    })
    .catch((error) => {
        console.error('Error:', error);
    });
```

---

## Exercise

Create new `html`, `css`, `js` and `json` files:

 - `data-simple.html`
 - `data-simple.json`
 - `data-simple.js`
 - `data-simple.css`

Add some HTML to `data-simple.html`:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="data-simple.css" />
        <script defer src="data-simple.js"></script>
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <h1>Planets of the solar system</h1>
        <div class="planets">
        </div>
    </body>
</html>
```

Add some CSS to `data-simple.css`:

```css
p {
    margin: 0;
}

.planet {
    border: 2px solid black;
    border-radius: 50%;
    height: 250px;
    width: 250px;
    padding: 10px;
    margin: 20px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    text-decoration: none;
    color: black;
}

.planet:hover {
    background: lightgrey;
    text-decoration: underline;
    color: blue;
}

.planet-image {
    max-width: 50%;
}

.planet-name {
    font-weight: bold;
    font-size: 24px;
}

.planet-circumference,
.planet-distance {
    font-style: italic;
}

/* Exercise 1 styles */

.planet-Earth {
    background: green;
}

.planet-Mars {
    background: red;
}

/* Exercise 2 styles */

.planet-earth {
    background: green;
}

.planet-mars {
    background: red;
}
```

Add some JavaScript to `data-simple.js`:

```js
function addPlanetToPage(planet) {
    // create a new element for each planet
    const planetElement = document.createElement("div");
    planetElement.classList.add("planet");
    planetElement.classList.add("planet-" + planet.name);

    // add the planet name
    const planetName = document.createElement("p");
    planetName.classList.add("planet-name");
    planetName.textContent = planet.name;
    planetElement.appendChild(planetName);

    // add other planet details
    const planetCircumference = document.createElement("p");
    planetCircumference.classList.add("planet-circumference");
    planetCircumference.textContent = "Circumference: " + planet.circumference;
    planetElement.appendChild(planetCircumference);

    const planetDistance = document.createElement("p");
    planetDistance.classList.add("planet-distance");
    planetDistance.textContent = "Distance from sun: " + planet.distanceFromSun;
    planetElement.appendChild(planetDistance);

    // add the planet to the page
    const planetListElement = document.querySelector(".planets");
    planetListElement.appendChild(planetElement);
}
```

So far, this is *exactly* the same code as we had in the exercise we completed earlier.

The only difference is that we haven't added our data into the same JS file as the logic above.

Instead, let's add it to the JSON file `data-simple.json`:

```json
[
    {
        "name": "Mercury",
        "circumference": "2,500 km",
        "distanceFromSun": "57,000,000 km"
    },
    {
        "name": "Venus",
        "circumference": "28,000 km",
        "distanceFromSun": "108,000,000 km"
    },
    {
        "name": "Earth",
        "circumference": "40,000 km",
        "distanceFromSun": "150,000,000 km"
    },
    {
        "name": "Mars",
        "circumference": "227,000,000 km",
        "distanceFromSun": "21,000 km"
    },
    {
        "name": "Jupiter",
        "circumference": "779,000,000 km",
        "distanceFromSun": "440,000 km"
    },
    {
        "name": "Saturn",
        "circumference": "1,430,000,000 km",
        "distanceFromSun": "365,000 km"
    },
    {
        "name": "Uranus",
        "circumference": "2,880,000,000 km",
        "distanceFromSun": "160,000 km"
    },
    {
        "name": "Neptune",
        "circumference": "4,500,000,000 km",
        "distanceFromSun": "154,000 km"
    }
]
```

Finally, we need to *fetch* this JSON and use it to call the `addPlanetToPage` function.

Add this to the JavaScript file `data-simple.js` below what you have already written:

```js
fetch('data-simple.json')
    .then((response) => response.json())
    .then((data) => {
        console.log('Data: ', data);

        // loop through each planet object in the array,
        // and add them to the page
        data.forEach(addPlanetToPage);
    })
    .catch((error) => {
        console.error('Error:', error);
    });
```

Open the HTML file in a web browser (e.g. Firefox). Also open the JavaScript console. Make sure that there aren't any errors being displayed.

The end result should be the same as what we put together in earlier, but we have successfully extracted our data and stored it separately.

If you get stuck, example files can be found here:

 - [data-simple.html](examples/data-simple/data-simple.html)
 - [data-simple.css](examples/data-simple/data-simple.css)
 - [data-simple.js](examples/data-simple/data-simple.js)
 - [data-simple.json](examples/data-simple/data-simple.json)


---

## Exercise

We are going to extend the example above.

We will add in extra content to our data by adding a link and an image to each piece of data.

We'll then learn how to create images and links with JavaScript.

Create new `html`, `js` and `json` files:

 - `data-complex.html`
 - `data-complex.css`
 - `data-complex.json`
 - `data-complex.js`

Here is the HTML - it's the same as the previous exercise, we've just renamed the JavaScript file that we're importing:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Planets of the solar system</title>
        <link rel="stylesheet" href="data-complex.css" />
        <script defer src="data-complex.js"></script>
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <h1>Planets of the solar system</h1>
        <div class="planets">
        </div>
    </body>
</html>
```

The CSS will be the same too so copy that over.

Here's our new JSON data. Notice that this has more information - we've now added extra pieces of data to each object, a class, an image and a link:

```json
[
    {
        "name": "Mercury",
        "class": "mercury",
        "circumference": "2,500 km",
        "distanceFromSun": "57,000,000 km",
        "url": "https://en.wikipedia.org/wiki/Mercury_(planet)",
        "image": "https://upload.wikimedia.org/wikipedia/commons/d/d9/Mercury_in_color_-_Prockter07-edit1.jpg"
    },
    {
        "name": "Venus",
        "class": "venus",
        "circumference": "28,000 km",
        "distanceFromSun": "108,000,000 km",
        "url": "https://en.wikipedia.org/wiki/Venus",
        "image": "https://upload.wikimedia.org/wikipedia/commons/a/a9/PIA23791-Venus-NewlyProcessedView-20200608.jpg"
    },
    {
        "name": "Earth",
        "class": "earth",
        "circumference": "40,000 km",
        "distanceFromSun": "150,000,000 km",
        "url": "https://en.wikipedia.org/wiki/Earth",
        "image": "https://upload.wikimedia.org/wikipedia/commons/9/97/The_Earth_seen_from_Apollo_17.jpg"
    },
    {
        "name": "Mars",
        "class": "mars",
        "circumference": "227,000,000 km",
        "distanceFromSun": "21,000 km",
        "url": "https://en.wikipedia.org/wiki/Mars",
        "image": "https://upload.wikimedia.org/wikipedia/commons/0/02/OSIRIS_Mars_true_color.jpg"
    },
    {
        "name": "Jupiter",
        "class": "jupiter",
        "circumference": "779,000,000 km",
        "distanceFromSun": "440,000 km",
        "url": "https://en.wikipedia.org/wiki/Jupiter",
        "image": "https://upload.wikimedia.org/wikipedia/commons/2/2b/Jupiter_and_its_shrunken_Great_Red_Spot.jpg"
    },
    {
        "name": "Saturn",
        "class": "saturn",
        "circumference": "1,430,000,000 km",
        "distanceFromSun": "365,000 km",
        "url": "https://en.wikipedia.org/wiki/Saturn",
        "image": "https://upload.wikimedia.org/wikipedia/commons/c/c7/Saturn_during_Equinox.jpg"
    },
    {
        "name": "Uranus",
        "class": "uranus",
        "circumference": "2,880,000,000 km",
        "distanceFromSun": "160,000 km",
        "url": "https://en.wikipedia.org/wiki/Uranus",
        "image": "https://upload.wikimedia.org/wikipedia/commons/3/3d/Uranus2.jpg"
    },
    {
        "name": "Neptune",
        "class": "neptune",
        "circumference": "4,500,000,000 km",
        "distanceFromSun": "154,000 km",
        "url": "https://en.wikipedia.org/wiki/Neptune",
        "image": "https://upload.wikimedia.org/wikipedia/commons/6/63/Neptune_-_Voyager_2_%2829347980845%29_flatten_crop.jpg"
    }
]
```

We'll start with the same JavaScript that we had at the end of the last exercise too - again just renaming the `JSON` file that we import:

```js
fetch('data-complex.json')
    .then((response) => response.json())
    .then((data) => {
        data.forEach(addPlanetToPage);
    })
    .catch((error) => {
        console.error('Error:', error);
    });


function addPlanetToPage(planet) {
    // create a new element for each planet
    const planetElement = document.createElement("div");
    planetElement.classList.add("planet");
    planetElement.classList.add("planet-" + planet.name);

    // add the planet name
    const planetName = document.createElement("p");
    planetName.classList.add("planet-name");
    planetName.textContent = planet.name;
    planetElement.appendChild(planetName);

    // add other planet details
    const planetCircumference = document.createElement("p");
    planetCircumference.classList.add("planet-circumference");
    planetCircumference.textContent = "Circumference: " + planet.circumference;
    planetElement.appendChild(planetCircumference);

    const planetDistance = document.createElement("p");
    planetDistance.classList.add("planet-distance");
    planetDistance.textContent = "Distance from sun: " + planet.distanceFromSun;
    planetElement.appendChild(planetDistance);

    // add the planet to the page
    const planetListElement = document.querySelector(".planets");
    planetListElement.appendChild(planetElement);
}
```

Open the HTML page in a browser. You should notice that it looks exactly the same as our previous exercise - although there is an image and link defined in the data, it doesn't change anything until we do something with this data.


### Updating the class

We currently use the following line of JavaScript to give each planet a unique class. This allows us to apply different styles to each planet:

```js
planetElement.classList.add("planet-" + planet.name);
```

However, there is a problem here - HTML classes can't contain spaces, so we would run into a problem if we wanted to use a name which was more than one word, it would cause an error in the console and our JavaScript wouldn't work.

To fix this, in our new JSON data for this exercise we have added an extra field containing a `class` that we can use instead, by replacing the line above with:

```js
planetElement.classList.add("planet-" + planet.class);
```

Defining a name and a class separately gives us greater flexibility, as it allows us to have a name that contained multiple words.

For example, we could add the following to the data - note how the name is two words, but the class remains a single word (hyphenated) so it doesn't break the JavaScript:

```json
    {
        "name": "The Moon",
        "class": "the-moon",
        "circumference": "10,921 km",
        "distanceFromSun": "150,000,000 km",
        "url": "https://en.wikipedia.org/wiki/Moon",
        "image": "https://upload.wikimedia.org/wikipedia/commons/e/e1/FullMoon2010.jpg"
    }
```

An alternative method to achieve a similar result could be to replace spaces with hyphens in the name before using it as a class:

```js
planetElement.classList.add("planet-" + planet.name.replace(" ", "-");
```


### Adding an image

The new JSON data now includes a URL to an image.

Remember that an HTML image element looks like this:

```html
<img src="image-url.jpg" alt="Image description" />
```

To create this with JavaScript we can use syntax similar to that we have already seen:

```js
// add planet image
const planetImage = document.createElement("img");
planetImage.classList.add("planet-image");
planetImage.src = planet.image;
planetImage.alt = "A photograph of the planet " + planet.name;
planetElement.appendChild(planetImage);
```

Note how we directly set the two attributes - `src` and `alt`.


### Adding a link

We have two options when adding a link - we can add the link as a new piece of text below the current content, or we can make the entire planet element a link.

#### Adding a text link

To add a new text link, we can follow a similar pattern to the image.

Remember that an HTML link looks like this:

```html
<a href="http://whatever.com">Link text</a>
```

To create this with JavaScript we could add:

```js
// add planet link
const planetLink = document.createElement("a");
planetLink.classList.add("planet-link");
planetLink.href = planet.url;
planetLink.textContent = "Read more about " + planet.name;
planetElement.appendChild(planetLink);
```


#### Making the entire planet element a link

Alternatively, we could convert the entire planet element into a link.

If you would like to do this, you should comment out (or remove) the link you just created above - web browsers get confused when you have a link within a link.

In our existing JavaScript, find the following line:

```js
const planetElement = document.createElement("div");
```

Change the `div` into an `a` link, and then add the link `href` too:

```js
const planetElement = document.createElement("a");
planetElement.href = planet.url;
```

That's it!


If you get stuck, example files can be found here:

 - [data-complex.html](examples/data-complex/data-complex.html)
 - [data-complex.css](examples/data-complex/data-complex.css)
 - [data-complex.js](examples/data-complex/data-complex.js)
 - [data-complex.json](examples/data-complex/data-complex.json)

---

## APIs

We now know how to load data from an external file and use it in our web page.

The advantage of this approach is that we can manage our data separately from the logic we write to build our websites.

We can now also start to look elsewhere for our data. We can load data from other sources into our web pages. There are third-party services that offer data, via an *API*.

When we load data from an external source, we won't know what content we'll be receiving. What we do know is the *structure* of that data.

For example, in the data that we used for the planets, we know that each item will have these values:

 - `"name"`
 - `"circumference"`
 - `"distanceFromSun"`
 - `"image"`
 - `"url"`

When we look at external APIs, we'll see that they provide documentation that gives us the structure of their data, so that we know how to use it once we've loaded it.

Below there are examples of some external APIs - how to read about the information they offer, and how to write the JavaScript code necessary to access them.

---


### API example: ISS

This API can be used to find the current location of the International Space Station.

 - Home page: [https://wheretheiss.at](https://wheretheiss.at)
 - Documentation: [https://wheretheiss.at/w/developer](https://wheretheiss.at/w/developer)
 - **JSON URL:** `https://api.wheretheiss.at/v1/satellites/25544`
 - [Example web page](examples/api-examples/api-iss.html)

Example response:

```json
{
    "name": "iss",
    "id": 25544,
    "latitude": 50.11496269845,
    "longitude": 118.07900427317,
    "altitude": 408.05526028199,
    "velocity": 27635.971970874,
    "visibility": "daylight",
    "footprint": 4446.1877699772,
    "timestamp": 1364069476,
    "daynum": 2456375.3411574,
    "solar_lat": 1.3327003598631,
    "solar_lon": 238.78610691196,
    "units": "kilometers"
}
```

Example HTML:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>API example: ISS</title>
        <link rel="stylesheet" href="api-iss.css" />
        <script defer src="api-iss.js"></script>
    </head>
    <body>
        <h1>API example: ISS</h1>
        <h2>ISS location</h2>
        <p><strong>Latitude:</strong> <em class="latitude"></em></p>
        <p><strong>Longitude:</strong> <em class="longitude"></em></p>
        <button class="update">Update ISS location</button>
    </body>
</html>
```

Example JavaScript:

```js
function requestISSLocation() {
    var apiUrl = "https://api.wheretheiss.at/v1/satellites/25544";

    fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
            console.log('Data :', data);

            // once we have the new ISS location, update the page
            updateISSLocation(data);
        })
        .catch((error) => {
            console.error('Error:', error);
        });
}

// update the latitude and longitude displayed on the page
function updateISSLocation(data) {
    var latitudeElement = document.querySelector(".latitude");
    latitudeElement.textContent = data.latitude;

    var longitudeElement = document.querySelector(".longitude");
    longitudeElement.textContent = data.longitude;
}

// listen for clicks on the button
var updateButton = document.querySelector('.update');
updateButton.addEventListener("click", requestISSLocation);

// also update location on page load
requestISSLocation();
```

Ideas for further work:

- Automatically update the current location every 10 seconds - use [`setTimeout()`](https://www.sitepoint.com/jquery-settimeout-function-examples/)
- Plot the location on a Google map

Source files:

 - [HTML](examples/api-examples/api-iss.html)
 - [CSS](examples/api-examples/api-iss.css)
 - [JS](examples/api-examples/api-iss.js)

---

### API example: Weather

This API can be used to display weather

 - Home page: [https://open-meteo.com/](https://open-meteo.com/)
 - Docs: [https://open-meteo.com/en/docs](https://open-meteo.com/en/docs)
 - **JSON URL:** `https://api.open-meteo.com/v1/forecast?latitude=50.815331&longitude=-0.136790&daily=temperature_2m_max,temperature_2m_min`
 - [Example web page](examples/api-examples/api-weather.html)


Response:

```json
{
    "latitude": 50.82,
    "longitude": -0.120000124,
    "generationtime_ms": 0.07998943328857422,
    "utc_offset_seconds": 0,
    "timezone": "GMT",
    "timezone_abbreviation": "GMT",
    "elevation": 0,
    "daily_units": {
        "time": "iso8601",
        "temperature_2m_max": "°C",
        "temperature_2m_min": "°C",
        "wind_speed_10m_max": "km/h",
        "precipitation_probability_mean": "%"
    },
    "daily": {
        "time": [
            "2024-04-14"
        ],
        "temperature_2m_max": [
            11.5
        ],
        "temperature_2m_min": [
            8.8
        ],
        "wind_speed_10m_max": [
            20.3
        ],
        "precipitation_probability_mean": [
            1
        ]
    }
}
```

Source files:

 - [HTML](examples/api-examples/api-weather.html)
 - [CSS](examples/api-examples/api-weather.css)
 - [JS](examples/api-examples/api-weather.js)

---

### API example: Dad jokes API

This API can be used to display dad jokes...

 - Home page: [https://icanhazdadjoke.com/api](https://icanhazdadjoke.com/api)
 - **JSON URL:** `https://icanhazdadjoke.com/`
 - [Example web page](examples/api-examples/api-joke.html)


Response:

```json
{
    "id": "LRnGeVfiNe",
    "joke": "Today a man knocked on my door and asked for a small donation towards the local swimming pool. I gave him a glass of water.",
    "status": 200
}
```

Source files:

 - [HTML](examples/api-examples/api-joke.html)
 - [CSS](examples/api-examples/api-joke.css)
 - [JS](examples/api-examples/api-joke.js)

Once the JavaScript is written, you can style the page to turn it into something more visually appealing:

 - [HTML](examples/api-examples/api-joke-styled.html)
 - [CSS](examples/api-examples/api-joke-styled.css)
 - [JS](examples/api-examples/api-joke-styled.js)


---

### Other APIs

These are just a few examples of public APIs that can be used.

There are *many* more. You can find some listed on the following websites:

   - [https://apilist.fun/](https://apilist.fun/)
   - [https://github.com/public-apis/public-apis](https://github.com/public-apis/public-apis)

Note that each of the API examples given above has been integrated in a slightly different way - they will all need a certain amount of custom configuration to get them to work.

If you find an API that doesn't work without a proxy (like the News API above) let me know and I can help you to resolve this issue.

---

## Advanced content filtering

we learnt how to filter content based on text input.

It may be that you would like to filter by clicking buttons rather than typing into a search field.

This example uses JSON to store our data about each planet, for example:

```json
[
  {
    "name": "Jupiter",
    "circumference": "779,000,000km",
    "distanceFromSun": "440,000km",
    "hasLife": false,
    "majorMoons": ["Io", "Europa", "Ganymede", "Calisto"],
    "atmosphere": ["Hydrogen", "Helium"]
  }
]
```

The HTML contains an input field for search, and also buttons for different types of atmosphere:

```html
<label>
    Search planets:
    <input type="text" name="search" class="search" placeholder="Enter words to search for" />
</label>
<div class="atmosphere-buttons">
    Filter planets by atmosphere:
    <button class="atmosphere-button currently-selected-button">All</button>
    <button class="atmosphere-button">Carbon Dioxide</button>
    <button class="atmosphere-button">Oxygen</button>
    <button class="atmosphere-button">Hydrogen</button>
</div>
```

The JavaScript is similar to what we have seen earlier.

There are a few new pieces of functionality, such as turning the array of `atmosphere` values into a single string using `.join()`:

```js
// Atmosphere
const planetAtmosphere = document.createElement("p");
planetAtmosphere.classList.add("planet-atmosphere");
if (planet.atmosphere.length > 0) {
    planetAtmosphere.textContent = "Atmosphere: " + planet.atmosphere.join(', ');
} else {
    planetAtmosphere.textContent = "No atmosphere";
}
planetElement.appendChild(planetAtmosphere);
```

There are two sets of event listeners in the JavaScript:

 - One listener for detecting when text is entered in the search field
 - Another set of listeners for detecting when any of the buttons are clicked

When any of these events occur, the search terms are updated, and then all planets are checked to see whether they should be shown or hidden.

 - [Example HTML](./examples/filter-buttons/filter-buttons.html)
 - [Example CSS](./examples/filter-buttons/filter-buttons.css)
 - [Example JS](./examples/filter-buttons/filter-buttons.js)
 - [Example JSON](./examples/filter-buttons/filter-buttons.json)

---

## Hamburger menus

- [Simple Example](./examples/hamburger/hamburger.html)
- [Advanced Example](./examples/hamburger-advanced/hamburger.html)
- [Full Screen Example](./examples/hamburger-fullscreen/hamburger.html)

You may wish to have a menu that is displayed on larger resolutions, but for lower resolutions (such as mobile screens) this is converted into a 'hamburger' menu.

The idea here is that you have a button that is shown only at lower resolutions:

```html
<div class="menu">
    <button class="menu-toggle">Menu</button>
    <ul class="menu-list">
        <li>
            <a href="#">Home</a>
        </li>
        <li>
            <a href="#">About</a>
        </li>
        <li>
            <a href="#">Contact</a>
        </li>
    </ul>
</div>
```

You can add some JavaScript that listens for clicks on the button, and adds a class to the menu which will help to identify when to show or hide it:

```js
// Toggle the menu visibility
function toggleMenu() {
  const menuElement = document.querySelector(".menu");
  menuElement.classList.toggle("is-visible");
}

// Add a listener to the button to toggle menu visibility on click
const menuToggleElement = document.querySelector(".menu-toggle");
menuToggleElement.addEventListener("click", toggleMenu);
```

And with CSS, you create some styles that will only show the menu when the browser is wide enough or the button is active:

```css
/* menu toggle */

@media (min-width: 1200px) {
  /* hide the menu toggle button when there is enough space on screen for full menu */
  .menu-toggle {
    display: none;
  }
}

/* menu list */

.menu-list {
  display: none; /* hide the list by default for lower resolutions */
}

.menu.is-visible .menu-list {
  display: block; /* display the list when the button is selected */
}

@media (min-width: 1200px) {
  /* at larger resolutions show the whole menu in a line, not as a dropdown */
  .menu-list {
    display: block;
  }
}
```

Note in the example above, the breakpoint is set at `1200px` in two places, but this can be changed easily to whatever works best for your design.

Here is an example implementation:

 - [Example HTML](./examples/hamburger/hamburger.html)
 - [Example CSS](./examples/hamburger/hamburger.css)
 - [Example JS](./examples/hamburger/hamburger.js)

Here is a more advanced implementation - the JavaScript is the same but this features more complex CSS styles for the button and menu:

 - [Example HTML](./examples/hamburger-advanced/hamburger.html)
 - [Example CSS](./examples/hamburger-advanced/hamburger.css)
 - [Example JS](./examples/hamburger-advanced/hamburger.js)

Here is a version where the open menu fills the full screen:

 - [Example HTML](./examples/hamburger-fullscreen/hamburger.html)
 - [Example CSS](./examples/hamburger-fullscreen/hamburger.css)
 - [Example JS](./examples/hamburger-fullscreen/hamburger.js)

---


## Speech synthesis

- [Example](./examples/speech/speech.html)
- [Advanced example](./examples/speech-advanced/speech.html)

You can generate speech with just three lines of JavaScript:

```js
const sayThis = new SpeechSynthesisUtterance("This is a test");
const synth = window.speechSynthesis;
synth.speak(sayThis);
```

The API for this is explained here:

[https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesis](https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesis)

Here is an example implementation:

 - [Example HTML](./examples/speech/speech.html)
 - [Example CSS](./examples/speech/speech.css)
 - [Example JS](./examples/speech/speech.js)

And a more advanced example implementation:

 - [Example HTML](./examples/speech-advanced/speech.html)
 - [Example CSS](./examples/speech-advanced/speech.css)
 - [Example JS](./examples/speech-advanced/speech.js)

---

## Countdown

- [Example](./examples/countdown/countdown.html)

A countdown is a fun way to add content to a web page that updates every second.

It uses a built-in browser function called `setTimeout()` to run our custom function every 1000 milliseconds (or one second).

Here is an example implementation:

 - [Example HTML](./examples/countdown/countdown.html)
 - [Example CSS](./examples/countdown/countdown.css)
 - [Example JS](./examples/countdown/countdown.js)

---

## Dark mode toggle

 - [Example](./examples/dark-mode-toggle/dark-mode-toggle.html)

Some users may prefer to have a page with a light background colour, with dark text. Others may prefer a dark background with light text.

This example lets you create a page with both options, and a toggle to switch between the two:

 - [Example HTML](./examples/dark-mode-toggle/dark-mode-toggle.html)
 - [Example CSS](./examples/dark-mode-toggle/dark-mode-toggle.css)
 - [Example JS](./examples/dark-mode-toggle/dark-mode-toggle.js)

---


## Geolocation

- [Simple example](./examples/geolocation/geolocation.html)
- [Advanced example](./examples/geolocation-advanced/geolocation.html)

You can use the browser's built-in `geolocation` API to request a user's current location. They don't have to share it with the website, but if they do you can do interesting things with it, such as plot it on a map or calculate the distance between their current location and another location.

Here is a simple example implementation:

 - [Example HTML](./examples/geolocation/geolocation.html)
 - [Example CSS](./examples/geolocation/geolocation.css)
 - [Example JS](./examples/geolocation/geolocation.js)

Here is an advanced example implementation with a map and a distance calculation:

 - [Example HTML](./examples/geolocation-advanced/geolocation.html)
 - [Example CSS](./examples/geolocation-advanced/geolocation.css)
 - [Example JS](./examples/geolocation-advanced/geolocation.js)


---

## Creating a quiz

- [Example](./examples/quiz/quiz.html)

Create three new files:

 - `quiz.html`
 - `quiz.css`
 - `quiz.js`

---

### Quiz - HTML

First, we need to create the HTML form for people to interact with.

We have seen how to use HTML form elements, these can be used for a quiz.

For example to create a list of radio buttons:

```html
<p>Question 1. Which planet has rings?</p>
<label>
    <input type="radio" name="question-1" value="Saturn">
    Saturn
</label>
<label>
    <input type="radio" name="question-1" value="Mercury">
    Mercury
</label>
<label>
    <input type="radio" name="question-1" value="Mars">
    Mars
</label>
```
This would generate the following form:

>
> <p>Question 1. Which planet has rings?</p>
<label>
    <input type="radio" name="question-1" value="Saturn">
    Saturn
</label>
<label>
    <input type="radio" name="question-1" value="Mercury">
    Mercury
</label>
<label>
    <input type="radio" name="question-1" value="Mars">
    Mars
</label>
>

---

To create an HTML select input:

```html
<p>Question 2. What is the closest planet to the sun?</p>
<select name="question-2">
    <option></option>
    <option>Saturn</option>
    <option>Mercury</option>
    <option>Mars</option>
</select>
```

This would generate:

>
> <p>Question 2. What is the closest planet to the sun?</p>
<select name="question-2">
    <option></option>
    <option>Saturn</option>
    <option>Mercury</option>
    <option>Mars</option>
</select>
>

---

To create an HTML text input:

```html
<p>Question 3. Which planet has life?</p>
<input type="text" name="question-3" value="">
```

This would generate:

>
> <p>Question 3. Which planet has life?</p>
<input type="text" name="question-3" value="">
>

---

For a submit button:

```html
<button>Go!</button>
```

This would generate:

>
> <button class="quiz-submit">Go!</button>
>

---

You could use a combination of the form elements above to create the questions for your quiz.

When someone finishes answering the questions and submits the form, we will want to check their answers against the correct answers, and show the result.

We've seen how to show and hide HTML elements, so we could create a different results element for each possible score, for example:

```html
<div class="quiz-result quiz-result-0">You answered 0 questions correctly</div>
<div class="quiz-result quiz-result-1">You answered 1 question correctly</div>
<div class="quiz-result quiz-result-2">You answered 2 questions correctly</div>
<div class="quiz-result quiz-result-3">You answered 3 questions correctly</div>
```

We would hide all of the above results by default with CSS, and then only show the relevant one for the correct score once we've worked out how many questions the user has answered correctly.

---

Here is an example of an HTML page that contains a quiz form with three quiz questions - you could copy this into your `quiz.html` file:

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>Quiz</title>
        <link rel="stylesheet" href="quiz.css" />
        <script defer src="quiz.js"></script>
    </head>
    <body>

        <h1>Quiz</h1>

        <form class="quiz">
            <div class="quiz-row">
                <p class="quiz-question">Question 1. Which planet has rings?</p>
                <div class="quiz-answers">
                    <label class="quiz-answer">
                        <input type="radio" name="question-1" value="Saturn" class="quiz-answer-radio">
                        Saturn
                    </label>
                </div>
                <div class="quiz-answers">
                    <label class="quiz-answer">
                        <input type="radio" name="question-1" value="Mercury" class="quiz-answer-radio">
                        Mercury
                    </label>
                </div>
                <div class="quiz-answers">
                    <label class="quiz-answer">
                        <input type="radio" name="question-1" value="Mars" class="quiz-answer-radio">
                        Mars
                    </label>
                </div>
            </div>

            <div class="quiz-row">
                <p class="quiz-question">Question 2. What is the closest planet to the sun?</p>
                <div class="quiz-answers">
                    <label class="quiz-answer">
                        <select name="question-2" class="quiz-answer-select">
                            <option></option>
                            <option>Saturn</option>
                            <option>Mercury</option>
                            <option>Mars</option>
                        </select>
                    </label>
                </div>
            </div>

            <div class="quiz-row">
                <p class="quiz-question">Question 3. Which planet has life?</p>
                <div class="quiz-answers">
                    <label class="quiz-answer">
                        <input type="text" name="question-3" value="" class="quiz-answer-text">
                    </label>
                </div>
            </div>

            <div class="quiz-buttons">
                <button type="button" class="quiz-submit">Go!</button>
                <button type="button" class="quiz-reset">Reset</button>
            </div>
        </form>

        <div class="quiz-results">
            <div class="quiz-result quiz-result-3">
                <h2 class="quiz-result-title">Well done, you answered all three questions correctly!</h2>
                <p class="quiz-result-text">You really know your space</p>
            </div>
            <div class="quiz-result quiz-result-2">
                <h2 class="quiz-result-title">Well done, you answered two questions correctly!</h2>
                <p class="quiz-result-text">You know some things about space</p>
            </div>
            <div class="quiz-result quiz-result-1">
                <h2 class="quiz-result-title">You answered one question correctly</h2>
                <p class="quiz-result-text">Not bad...</p>
            </div>
            <div class="quiz-result quiz-result-0">
                <h2 class="quiz-result-title">Oh dear, you got all questions wrong!</h2>
                <p class="quiz-result-text">Better luck next time!</p>
            </div>
        </div>

    </body>
</html>
```

<br>
---

### Quiz - CSS

We could add CSS to style the different form elements, but actually the only CSS we need to add initially is to hide the score elements we just created:

```css
/* hide all scores when the page loads */
.quiz-result {
    display: none;
}
```

When someone submits the form, we'll use JavaScript to check their answers and work out which of the scores to display. We'll do this by adding a class of `show` to the relevant score element:

```css
/* show only the correct score
note that the extra class "show" will be added dynamically by JavaScript */
.quiz-result.show {
    display: block;
}
```
<br>
---

Here is an example of a CSS file that would style the HTML we saw above, you could copy this into your `quiz.css` file:

```css
.quiz {
    background: lavender;
    padding: 10px;
}

.quiz-row {
    border-bottom: 2px solid black;
    margin-top: 10px;
    margin-bottom: 10px;
    padding: 10px;
}

.quiz-question {
    font-size: 18px;
    font-weight: bold;
}

.quiz-answer {
    display: block;
    font-size: 18px;
    margin-bottom: 10px;
}

.quiz-answer-select {
    font-size: 18px;
}

.quiz-answer-text {
    font-size: 18px;
    padding: 10px;
}

.quiz-submit {
    padding: 20px 50px;
    background: orange;
    border: none;
    cursor: pointer;
    color: white;
    font-size: 20px;
    margin-right: 20px;
}

.quiz-reset {
    padding: 20px 50px;
    background: lightgrey;
    border: none;
    cursor: pointer;
    color: black;
    font-size: 20px;
}

.quiz-result {
    display: none;
}

.quiz-result.show {
    display: block;
}
```

<br>
---

### Quiz - JavaScript

Now that we have created our HTML form and learnt how to style it, we want to check the answers that have been submitted.

The first thing we need to do is find our form submit buttons and add *event listeners* so we know when they have been clicked:

```js
const quizSubmitButton = document.querySelector(".quiz-submit");
quizSubmitButton.addEventListener("click", checkQuizAnswers);

function checkQuizAnswers(e) {
    // we'll add code here shortly...
}
```
The example above will call the function `checkQuizAnswers();` every time someone clicks the button. So we want to write our quiz-checking logic inside this function.

***Note that all of the following code examples should be added to the end of the `checkQuizAnswers()` function.***

Next, we're going to start calculating the user's quiz score. We start by creating a variable to remember their scopre, and also assuming they haven't got any questions correct yet.

```js
    // keep track of the current quiz score
    let score = 0;
```

Now we need to check the answers submitted for each quiz question. For example, if the question was a choice of radio buttons we need to work out which one was selected, and check the submitted answer against the answer we were expecting. If they got it correct, we increment the score:

```js
    // find the submitted answers:
    // question 1 is several radio inputs, so find the selected one
    // it may be that someone clicked submit without selecting a radio button,
    // so we need to see if one has been selected, and if so what its value is
    const question1 = document.querySelector("input[name=question-1]:checked");
    if (question1 && question1.value === "Saturn") {
        score = score + 1;
    }
```

This is how we would check the answer if the form input were a select dropdown list rather than a set of radio buttons:

```js
    // question 2 is a select dropdown element, so find the selected option
    const question2 = document.querySelector("select[name=question-2]").value;
    if (question2 === "Mercury") {
        score = score + 1;
    }
```

And this is how we would check the answer if the form input were a text input field. Note that because this is a text entry field we're allowing people to use *UPPERCASE* or *lowercase* letters, and also trimming any extra spaces they may have entered:

```js
    // question 3 is a text input
    // because this is a text entry field, allow people to use a capital or
    // lower-case, e.g. they can enter "Earth" or "earth"
    // also remove any spaces before or after, so they can enter " earth "
    const question3 = document.querySelector("input[name=question-3]").value;
    if (question3.trim().toLowerCase() === "earth") {
        score = score + 1;
    }
```

We now know what score our user has, it may be 0, 1, 2 or 3. (Yours will be different if you have more questions.) We want to display the correct results block based on their score:

```js
    // find the relevant quiz results block to display, based on their score
    const quizResultsBlock = document.querySelector(".quiz-result-" + score);
    quizResultsBlock.classList.add("show");
```


<br>
---

Here is our final JavaScript file that you could copy into `quiz.js` - note that it has a few extra steps, such as allowing the form to be reset so that the quiz can be attempted multiple times.

```js
// add listeners for the quiz buttons
const quizSubmitButton = document.querySelector(".quiz-submit");
quizSubmitButton.addEventListener("click", checkQuizAnswers);

const quizResetButton = document.querySelector(".quiz-reset");
quizResetButton.addEventListener("click", resetQuiz);


function checkQuizAnswers(e) {
    // stop the form submission refreshing the page, which is the default
    // behaviour when someone submits an HTML form
    e.preventDefault();

    // keep track of the current quiz score
    let score = 0;

    // find the submitted answers:
    // question 1 is several radio inputs, so find the selected one
    // it may be that someone clicked submit without selecting a radio button,
    // so we need to see if one has been selected, and if so what its value is
    const question1 = document.querySelector("input[name=question-1]:checked");
    if (question1 && question1.value === "Saturn") {
        score = score + 1;
    }

    // question 2 is a select dropdown element, so find the selected option
    const question2 = document.querySelector("select[name=question-2]").value;
    if (question2 === "Mercury") {
        score = score + 1;
    }

    // question 3 is a text input
    // because this is a text entry field, allow people to use a capital or
    // lower-case, e.g. they can enter "Earth" or "earth"
    // also remove any spaces before or after, so they can enter " earth "
    const question3 = document.querySelector("input[name=question-3]").value;
    if (question3.trim().toLowerCase() === "earth") {
        score = score + 1;
    }

    // hide the quiz results block if it is currently shown
    const quizResultsBlock = document.querySelector(".quiz-result.show");
    if (quizResultsBlock) {
        quizResultsBlock.classList.remove("show");
    }

    // find the relevant quiz results block to display, based on their score
    const quizResultsBlock = document.querySelector(".quiz-result-" + score);
    quizResultsBlock.classList.add("show");
}


function resetQuiz(e) {
    // stop the form submission refreshing the page, which is the default
    // behaviour when someone submits an HTML form
    e.preventDefault();

    // hide the quiz results block if it is currently shown
    const quizResultsBlock = document.querySelector(".quiz-result.show");
    if (quizResultsBlock) {
        quizResultsBlock.classList.remove("show");
    }

    // reset the first question - deselect the radio input if one is selected
    const question1 = document.querySelector("input[name=question-1]:checked");
    if (question1) {
        question1.checked = false;
    }

    // reset the second question - the select input
    const question2 = document.querySelector("select[name=question-2]");
    question2.value = "";

    // reset the third question - the text input
    const question3 = document.querySelector("input[name=question-3]")
    question3.value = "";
}
```

You can see the final working version here:

 - [HTML](./examples/quiz/quiz.html)
 - [CSS](./examples/quiz/quiz.css)
 - [JavaScript](./examples/quiz/quiz.js)


### Quiz - Further reading

You can find another (similar but more complicated) tutorial of how to create a quiz here:

 - [https://simplestepscode.com/javascript-quiz-tutorial/](https://simplestepscode.com/javascript-quiz-tutorial/)
