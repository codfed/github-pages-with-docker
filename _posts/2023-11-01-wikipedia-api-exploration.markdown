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

<table id="recentChangesTable">
  <thead>
    <th> Title </th>
    <th> Comment </th>
    <th> User </th>
    <th> Revision diff </th>
  </thead>
  <tbody>
  </tbody>
</table>

<button type="button" onclick="getRecentChanges()">
  Get 10 latest edits
</button>

<script>
  function getRecentChanges(){
    document.getElementById('recentChangesTable').innerHTML = '';

    var url = "https://en.wikipedia.org/w/api.php?action=query&origin=*&rctype=edit&rcprop=title|ids|rctype|comment|user|tags|flags&list=recentchanges&format=json";

    fetch(url)
      .then((response) => response.json())
      .then((json) => {
        for (var i in json.query.recentchanges) {
          let title = json.query.recentchanges[i].title;
          let pageid = json.query.recentchanges[i].pageid;
          let comment = json.query.recentchanges[i].comment;
          let user = json.query.recentchanges[i].user;
          let old_revid = json.query.recentchanges[i].old_revid;

          addChangesRow(title, pageid, comment, user, old_revid);
        }
      });  
  }

  function addChangesRow(title, pageid, comments, user, old_revid) {
    let table = document.getElementById("recentChangesTable");
  
    // Create a row using the inserRow() method and
    // specify the index where you want to add the row
    let row = table.insertRow(-1); // We are adding at the end
  
    // Create table cells
    let c1 = row.insertCell(0);
    let c2 = row.insertCell(1);
    let c3 = row.insertCell(2);
    let c4 = row.insertCell(3);

    // Build page link
    let pageLink = document.createElement('a');
    
    pageLink.setAttribute('href',"http://en.wikipedia.org/?curid=" + pageid);
    pageLink.setAttribute('target', '_blank');
    pageLink.innerText = title;

    // Build revision link
    let revisionURL = "https://en.wikipedia.org/w/index.php?title=" + title + "&diff=prev&oldid=" + old_revid
    let revisionLink = document.createElement('a');

    revisionLink.setAttribute('href', revisionURL);
    revisionLink.setAttribute('target', '_blank');
    revisionLink.innerText = "Revision Diff"; 
//https://en.wikipedia.org/w/index.php?title=Anastasia_(1997_film)&diff=prev&oldid=1183171127
  //  ?title=Anastasia_(1997_film)&diff=prev&oldid=1183171127

    // Add data to c1 and c2
    c1.appendChild(pageLink);
    c2.innerText = comments;
    c3.innerText = user;
    c4.appendChild(revisionLink);
   }
</script>


<table id="recentBlocksTable">
  <thead>
    <th> User </th>
    <th> Reason </th>
    <th> Expiry </th>
    <th>  </th>
  </thead>
  <tbody>
  </tbody>
</table>

<button type="button" onclick="getRecentBlocks()">
  Get 500 latest blocks
</button>

<script>
  function getRecentBlocks(){
    document.getElementById('recentBlocksTable').innerHTML = '';

    var url = "https://en.wikipedia.org/w/api.php?action=query&origin=*&list=blocks&formatversion=2&bkdir=older&bklimit=500&format=json";

    fetch(url)
      .then((response) => response.json())
      .then((json) => {
        for (var i in json.query.blocks) {
          let user = json.query.blocks[i].user;
          let reason = json.query.blocks[i].reason;
          let expiry = json.query.blocks[i].expiry;
          let by = json.query.blocks[i].by;
          // let old_revid = json.query.blocks[i].old_revid;

          addBlockRow(user, reason, expiry, by);
        }
      });  
  }

  function addBlockRow(user, reason, expiry, by) {
    let table = document.getElementById("recentBlocksTable");
  
    // Create a row using the inserRow() method and
    // specify the index where you want to add the row
    let row = table.insertRow(-1); // We are adding at the end
  
    // Create table cells
    let c1 = row.insertCell(0);
    let c2 = row.insertCell(1);
    let c3 = row.insertCell(2);
    let c4 = row.insertCell(3);

    // Build user page link
    let userPageLink = document.createElement('a');
    
    userPageLink.setAttribute('href',"http://en.wikipedia.org/wiki/User:" + user);
    userPageLink.setAttribute('target', '_blank');
    userPageLink.innerText = user;

    // Build by user page link
    let byUserPageLink = document.createElement('a');
    
    byUserPageLink.setAttribute('href',"http://en.wikipedia.org/wiki/User:" + by);
    byUserPageLink.setAttribute('target', '_blank');
    byUserPageLink.innerText = by;

    // Build revision link
    // let revisionURL = "https://en.wikipedia.org/w/index.php?title=" + title + "&diff=prev&oldid=" + old_revid
    // let revisionLink = document.createElement('a');

    // revisionLink.setAttribute('href', revisionURL);
    // revisionLink.setAttribute('target', '_blank');
    // revisionLink.innerText = "Revision Diff"; 
//https://en.wikipedia.org/w/index.php?title=Anastasia_(1997_film)&diff=prev&oldid=1183171127
  //  ?title=Anastasia_(1997_film)&diff=prev&oldid=1183171127

    // Add data to c1 and c2
    c1.appendChild(userPageLink);
    c2.innerText = reason;
    c3.innerText = expiry;
    c4.appendChild(byUserPageLink);
    // c4.appendChild(revisionLink);
   }
</script>

This actually came to fruition quicker than I had expected. The next few things I want to do are:

- SPECIFIC QUERY
- only vandalism
- only banned users
(25 most recent blocks) https://www.mediawiki.org/w/api.php?action=query&format=json&list=blocks&formatversion=2&bkdir=older&bklimit=25

- Make user profile page

- Play around with a react app to display data



<!-- ```html

```

```javascript

``` -->