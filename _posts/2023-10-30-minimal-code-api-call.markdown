---
layout: post
title:  "Calling an API fast track"
---

Minimal kind of feels like an oxymoron in a Ruby-based framework. Because if it were truly 'minimal', it would be a very simple html file. Now that I have that caveat spelled out, let's figure out how to call an API from this file...

In order to call a javascript function, I'll add a button using markdown.

Searching for Jekyll button markdown, I found this as a suggestion: `[Click me](){: .btn}`

[Click me](){: .btn}

If you inspect that element, you see that it is a link tag with the class 'btn'. That would be good enough to add an onclick function to then stylize it... but instead, I'll just use a regular html button.

`<button type="button">This button will do nothing!</button>`

<button type="button">This button will do nothing!</button>

---

Ok coool! I have a button that looks like a button and when I click it, the style changes to indicate it has been clicked. Let's add some javascript to make it work.

```html
<button type="button" onclick="showAlert()">This button will show an alert!</button>
```

```javascript
function showAlert(){
  alert("Showing this alert!");
}
```

<button type="button" onclick="showAlert()">This button will show an alert!</button>

<script>
  function showAlert(){
    alert("Showing this alert!");
  }
</script>

---

One of the many public APIs available that does not require a key is [catfact.ninja](https://catfact.ninja/fact). It returns a simple json response with two elements, the fact and the number of characters in the fact.

```json
{
  "fact":"A cat's hearing is much more sensitive than humans and dogs.",
  "length":60
}
```

Here's what we need to make this happen:
- Add a span to display the fact
- Submit API request
- Update span with cat fact

```html
<button type="button" onclick="callAPI()">
  This button will teach you more about cats!
</button>

<span id="APIResponse">
  Cat fact will display here
</span>
```

```javascript
function callAPI(){
  fetch("https://catfact.ninja/fact")
    .then((response) => response.json())
    .then((json) => {
      document.getElementById("APIResponse").textContent=json["fact"];
    });  
}
```

<button type="button" onclick="callAPI()">
  This button will teach you more about cats!
</button>

<span id="APIResponse">
  Cat fact will display here
</span>

<script>
  function callAPI(){
    fetch("https://catfact.ninja/fact")
      .then((response) => response.json())
      .then((json) => {
        document.getElementById("APIResponse").textContent=json["fact"];
      });  
  }
</script>
