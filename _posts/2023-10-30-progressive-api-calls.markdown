---
layout: post
title:  "Progressive API Calls"
---

I've tied into numerous, business critical APIs over the years. To this day, I maintain their functionality and periodically need to tweak things surrounding them. It's been a while since I set a brand call up from scratch so I want to play around with them while documenting the process.

We need to use Javascript to call the API. In order to call a javascript function, I'll add a button using markdown.

Searching for Jekyll button markdown, I found this as a suggestion: `[Click me](){: .btn}`

[Click me](){: .btn}

If you inspect that element, you see that it is an empty link tag with the class 'btn'. That would be good enough to add an onclick function to then stylize it... but instead, I'll just use a regular html button.

```html
<button type="button">This button will do nothing!</button>
```

<button type="button">This button will do nothing!</button>

---

## Let's put the button to work

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

## Let's connect the button to the API

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
<button type="button" onclick="callCatAPI()">
  This button will teach you more about cats!
</button>

<span id="CatAPIResponse">
  Cat fact will display here
</span>
```

```javascript
function callCatAPI(){
  fetch("https://catfact.ninja/fact")
    .then((response) => response.json())
    .then((json) => {
      document.getElementById("CatAPIResponse").textContent=json["fact"];
    });  
}
```

<button type="button" onclick="callCatAPI()">
  This button will teach you more about cats!
</button>

<span id="CatAPIResponse">
  Cat fact will display here
</span>

<script>
  function callCatAPI(){
    fetch("https://catfact.ninja/fact")
      .then((response) => response.json())
      .then((json) => {
        document.getElementById("CatAPIResponse").textContent=json["fact"];
      });  
  }
</script>

---

## Basic Wikpedia query

I have long been intrigued by the inner workings of Wikipedia, the unfathomable hours of community effort that goes into maintaing such a project, and the culture/drama within it. I'll likely go into this more in-depth in a future post. For now, I'll spare you the details and just show how to use the API.

If you submit this **request:**

`https://en.wikipedia.org/w/api.php?action=query&origin=*&format=json&generator=search&gsrnamespace=0&gsrlimit=5&gsrsearch='ChatGPT'`

Wikipedia returns these **results:**

```json
{
  "batchcomplete": "",
  "continue": {
    "gsroffset": 5,
    "continue": "gsroffset||"
  },
  "query": {
    "pages": {
      "48795986": {
        "pageid": 48795986,
        "ns": 0,
        "title": "OpenAI",
        "index": 5
      },
      "64695824": {
        "pageid": 64695824,
        "ns": 0,
        "title": "GPT-3",
        "index": 4
      },
      "72417803": {
        "pageid": 72417803,
        "ns": 0,
        "title": "ChatGPT",
        "index": 1
      },
      "72861474": {
        "pageid": 72861474,
        "ns": 0,
        "title": "GPT-4",
        "index": 2
      },
      "73363598": {
        "pageid": 73363598,
        "ns": 0,
        "title": "Bard (chatbot)",
        "index": 3
      }
    }
```

This list contains the 5 most releveant pages. The ordering here is alphabetical but the `index` element specifies their relevance. `index` is used by default when parsing through the results using javascript. 

I want to display this list as a bulleted list. So I will change the results span into a results ul.

```html
<button type="button" onclick="callWikipediaAPI()">
  This button will get the 5 most relevant pages to 'ChatGPT'!
</button>

<ul id="WikipediaAPIResponse">
  <li>Links to relevant pages will appear here</li>
</ul>
```

Programatically, this is more complicated than retrieving and displaying a cat fact, but not that bad. Since there are multiple results, we want to iterate through and perform the following operations
- build `<a>` tags using `title` as the link text and `pageid` as the target
- create new `<li>` elements
- append `<a>` element to `<li>` element
- append `<li>` element to `<ul>` list

```javascript
function callWikipediaAPI(){
  var url = "https://en.wikipedia.org/w/api.php?action=query&origin=*&format=json&generator=search&gsrnamespace=0&gsrlimit=5&gsrsearch='ChatGPT'";

  fetch(url)
    .then((response) => response.json())
    .then((json) => {
      var list = document.getElementById("WikipediaAPIResponse");
      list.innerHTML = "";
      for (var i in json.query.pages) {
        let li = document.createElement('li');
        let link = document.createElement('a');
        
        link.setAttribute('href',"http://en.wikipedia.org/?curid=" + json.query.pages[i].pageid);
        link.setAttribute('target', '_blank');
        link.innerText = json.query.pages[i].title;
        
        li.appendChild(link);
        list.appendChild(li);
      }
    });  
}
```

<button type="button" onclick="callWikipediaAPI()">
  This button will get the 5 most relevant pages to 'ChatGPT'!
</button>

<ul id="WikipediaAPIResponse">
  <li>Links to relevant pages will appear here</li>
</ul>

<script>
  function callWikipediaAPI(){
    var url = "https://en.wikipedia.org/w/api.php?action=query&origin=*&format=json&generator=search&gsrnamespace=0&gsrlimit=5&gsrsearch='ChatGPT'";

    fetch(url)
      .then((response) => response.json())
      .then((json) => {
        var list = document.getElementById("WikipediaAPIResponse");
        list.innerHTML = "";
        for (var i in json.query.pages) {
          let li = document.createElement('li');
          let link = document.createElement('a');
          
          link.setAttribute('href',"http://en.wikipedia.org/?curid=" + json.query.pages[i].pageid);
          link.setAttribute('target', '_blank');
          link.innerText = json.query.pages[i].title;
          
          li.appendChild(link);
          list.appendChild(li);
        }
      });  
  }
</script>

## Passing input to API

We now know that we can write code to access APIs. Now we need to allow the end user to tweak how the page interacts with the website. This also introduces something we haven't had to worry about so far.... human error.

<input type="text" id="DynamicWikipediaInput" >
<button type="button" onclick="callDynamicWikipediaAPI()">
  Search Wikipedia
</button>

<ul id="DynamicWikipediaAPIResponse">
  <li>Links to relevant pages will appear here</li>
</ul>

<script>
  function callDynamicWikipediaAPI(){
    var query = document.getElementById("DynamicWikipediaInput").value;
    var url = "https://en.wikipedia.org/w/api.php?action=query&origin=*&format=json&generator=search&gsrnamespace=0&gsrlimit=5&gsrsearch='" + query + "'";

    fetch(url)
      .then((response) => response.json())
      .then((json) => {
        var list = document.getElementById("DynamicWikipediaAPIResponse");
        list.innerHTML = "";
        for (var i in json.query.pages) {
          let li = document.createElement('li');
          let link = document.createElement('a');
          
          link.setAttribute('href',"http://en.wikipedia.org/?curid=" + json.query.pages[i].pageid);
          link.setAttribute('target', '_blank');
          link.innerText = json.query.pages[i].title;
          
          li.appendChild(link);
          list.appendChild(li);
        }
      });  
  }
</script>

<!-- ```html

```

```javascript

``` -->