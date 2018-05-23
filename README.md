# Listening to Nodes

## Objectives

1. Add an event listener to a DOM node

2. Trigger event listeners on DOM nodes

3. Explain the difference between bubbling and capturing events

### Instructions for In-Browser Learn IDE Users

If you are using the Learn IDE available in your browser, you will automatically
clone down the files you need when you click 'Open IDE', but in order to view
`index.html`, you will need to use `httpserver` to serve the HTML page
temporarily.  In the terminal, type `httpserver` and press enter. You will see
that `Your server is running at ...` followed by a string of numbers and dots.
This string is a temporary IP address that is hosting your `index.html` file.
Copy this string of numbers, open a new tab and past the string in to the URL
bar.

## Say what?

We've seen that we can easily manipulate nodes in the DOM, and even create and
remove elements at will. But how do we interact with nodes on the page?

Well, we _listen_ for them.

## `addEventListener()`

Adding an event listener to a DOM node is easy — we just call
`addEventListener()` on the node. `addEventListener()` takes two arguments: the
name of the event, and a function to handle the event.

Let's start by adding a listener for `click` events to the `main#main` element
in `index.html`. Once you've opened `index.html` in the browser, enter the
following in the browser's dev tools console:

```js
const main = document.querySelector('#main')

main.addEventListener('click', function(event) {
  alert('I was clicked!')
})
```

Now if you click on the `main` element (you can click its text, "My ID is
'main'!"), you should see an alert: `'I was clicked!'. What's going on here?`

The first argument, `'click'` is, as we've said, the name of the event we're
listening for. Click events probably make up a majority of events listened to,
but other common events are `change`, `'keydown'`, `'keyup'`, `'load'`,
`'mouseover'`, `'mouseout'` — the list goes on. You can find a reasonably
comprehensive list on
[MDN](https://developer.mozilla.org/en-US/docs/Web/Events).

The second argument is a function that accepts the event as its argument. When
you're browsing Amazon, for instance, and click to add something to your cart,
an event listener  on the 'Add to Cart' button fires, and the 'click' event is
registered.  The _event_ has a bunch of information attached to it - where the
mouse is on the screen, all the information about the _button_ you clicked, and
may even have information about the product you're looking at, like it's product
ID number.  All this information is wrapped up together in the _event_, then
passed in as an argument to the function _we write_, where we will be able to
access all that event info.

Each type of event has a number of useful, and unique properties on it —
keypress, keydown, and keyup events, for example, will have a `which` property
that tells us which key was pressed. Let's add an event listener to the `input`
element to get a feel for this.

```js
const input = document.querySelector('input')

input.addEventListener('keydown', function(e) {
  console.log(e.which)
})
```

Paste this code into the dev tools console in your browser, then start typing
keys inside the input field on `index.html`.  You should see numbers being
logged in the console. You'll notice that, for example, pressing "enter" prints
`13` in console; pressing "a" prints `65`; etc.. You've created a _keydown_
event! If you've ever played a web game where you use the keys to move something
around.. _this_ is how we get the keys to interact with the game.

## Preventing the default behavior

Refresh the page. We've got a vendetta against the letter "g" (71), so we're
going to prevent the input from receiving "g"s. Enter the following in your
console:

```js
const input = document.querySelector('input')

input.addEventListener('keydown', function(e) {
  if (e.which === 71) {
    return e.preventDefault()
  }
})
```

Now try to enter "g" in the input — no can do!

Every DOM `event` comes with a `preventDefault` property — `preventDefault` is a
function that, when called, will prevent the, well, default event from taking
place. It provides us an opportunity to intercept and tweak user interactions
(usually in more helpful ways than preventing them from typing "g").

Another, related event property is called `stopPropagation`. Like
`preventDefault`, `stopPropagation` is a function that, when called, interrupts
the event's normal behavior. In this case, it stops the event from triggering
other nodes in the DOM that might be listening for the same event.

Wait. Do we mean one action can trigger multiple events?

Yep.

## Review

We covered a lot in this lesson. Feel free to edit `index.html`, to write code
directly in the document (just put it between `<script></script>` tags), and to
play around with different events. It's important to practice so you can get the
hang of it!

You should now understand how to add an event listener, how different event
triggers work, and how to intercept user interactions with `e.preventDefault()`.


## Resources

- [MDN - Web Events](https://developer.mozilla.org/en-US/docs/Web/Events)
- [StackOverflow - Bubbling and Capturing](http://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing)
- [QuirksMode - Event order](http://www.quirksmode.org/js/events_order.html)
