---
layout: post
title:  "Wikipedia API Exploration"
---

Ok, now we have the wikipedia search page replicated in a considerably less useful way than on their website. My first goal in this exploration is to find clever vandalism. Who knows where I'll wind up along the way.

This is where I left off last time: [Progressive API Calls]({{ site.url }}/github-pages-with-docker/2023/10/30/progressive-api-calls )

## Finding edits
I found this [recent changes](https://www.mediawiki.org/w/api.php?action=help&modules=query%2Brecentchanges) api documentation. Through some trial and error, I came up with this query which gets the ten most recent edits.

 `https://www.mediawiki.org/w/api.php?action=query&rctype=edit&rcprop=title|ids|rctype|comment|user|tags|flags&list=recentchanges`

I'm going to parse through these and make links to the relevant pages.

Only one problem... when I run that request through javascript I get this error:

![cors error]({{ site.url }}/github-pages-with-docker/assets/images/cors-error.png)

But why? I used a very similar call in the previous post with no issues. After reviewing the queries side by side, I noticed I did not include the `origin=&` parameter. Once I added that I was back on my way!

<button type="button" onclick="getRecentChanges()">
  Get 10 latest edits
</button>

<ul id="RecentChangesResponse">
  <li>Recent Edits</li>
</ul>

<script>
  function getRecentChanges(){
    var query = document.getElementById("RecentChangesResponse").value;
    var url = "https://en.wikipedia.org/w/api.php?action=query&origin=*&rctype=edit&rcprop=title|ids|rctype|comment|user|tags|flags&list=recentchanges&format=json";
    // var url = "https://en.wikipedia.org/w/api.php?action=query&origin=*&format=json&generator=search&gsrnamespace=0&gsrlimit=5&gsrsearch='ChatGPT'";

    fetch(url)
      .then((response) => response.json())
      .then((json) => {
        var list = document.getElementById("RecentChangesResponse");
        list.innerHTML = "";
        for (var i in json.query.recentchanges) {
          let li = document.createElement('li');
          let link = document.createElement('a');
          let comment_span = document.createElement('span');
          
          link.setAttribute('href',"http://en.wikipedia.org/?curid=" + json.query.recentchanges[i].pageid);
          link.setAttribute('target', '_blank');
          link.innerText = json.query.recentchanges[i].title;


          comment_span.innerText = "(" + json.query.recentchanges[i].comment + ")";
          
          li.appendChild(link);
          li.appendChild(comment_span);
          list.appendChild(li);
        }
      });  
  }
</script>

This actually came to fruition quicker than I had expected. The next few things I want to do are:

- Be more specific in query, to only get vandalism
- Create a link to the difference they reverted
- Rework display of data as this list has quickly become too complex for this simple approach

<!-- ```html

```

```javascript

``` -->