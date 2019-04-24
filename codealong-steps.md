
1.  Inline JavaScript (least desirable).
```html
  <body onload="window.alert('welcome to my app!');">
```
2. Include script tags in our HTML documents. This technique is used primarily when generating content/properties through a back-end language. Try to avoid this if not necessary.
```html
  <html>
    <head>
      <script>
         alert('Welcome to my app!');
      </script>
    </head>
    <body>
    </body>
  </html>
```
3. Including the JavaScript file [at the footer] of our site/app.

**It is important to get used to falling in the habit of only doing DOM related manipulation only once our content has loaded.** This is required, as we can't manipulate something that has not yet been drawn in the browser. In plain JavaScript, we can usually wrap this in a 'window.onload' function.

```js
   // run this function when the document is loaded
   window.onload = function() {

     // create a couple of elements in an empty HTML page
     var main_heading = document.createElement("h1");
     var heading_text = document.createTextNode("Hello dynamic world!");
     main_heading.appendChild(heading_text);
     document.body.appendChild(main_heading);
  }
```

The above `window.onload` function adds a new element to our page through the following steps:

  1. We first create the new H1 element through the `document.createElement` method.
  2. We create the text through the `createTextNode` method.
  3. The text is added to the newly created H1 element.
  4. The H1 element is added to the body. Both steps 3 and 4 use the `appendChild` method to the respective element. Think of `appendChild` as an array of elements belonging to the element we are adding to.

Below are a few of the core interfaces to target existing elements in the DOM.

```html
<body>
  <div id="hello">Hello world</p>
  <ul id="gaCampuses">
    <li>DC</li>
    <li>NY</li>
    <li>SF</li>
    <li>LA</li>
    <li>HK</li>
  </ul>
</body>
```

```js
   // run this function when the document is loaded
   window.onload = function() {
     // Target items by id via the getElementById() method
     var helloElem = document.getElementById("hello");
     // We can access that element's css styles through the style property, and then accessing the css property through its camel-cased equivalent
     helloElem.style.color = "red";

     var campusesContainer = document.getElementById("gaCampuses");
     // The getElementsByTagName() method returns a live HTMLCollection of elements with the given tag name.
     var gaCampuses = campusesContainer.getElementsByTagName("li");

     // We can iterate through the returned collection with a for loop
     for (var i = 0; i < gaCampuses.length; i++) {
          gaCampuses[i].style.backgroundColor = "red";
      }
  }
```

Finally, we can set certain events to execute based on user interaction. A common example is listening for a button click.

```html
  <form>
    <input id="my-input" />
    <input id="my-input-button" type="submit" value="Run button code"></submit>
  </form>
```

```js
  window.onload = function() {
    button = document.getElementById('my-input-button');
    // Event parameter is the default object event that would have happened on user click
    button.onclick = function(event) {
      // The preventDefault() method lets us disable the default action, allowing us to override with our on functionality.
      event.preventDefault();
      MyApp.do_something("world");
    };
  };

  // We can define things outside of the `window.onload` that are evaluated
  // only when called.
  MyApp = {};

  MyApp.do_something = function(name) {
    console.log("Hello " + name);
  }
```