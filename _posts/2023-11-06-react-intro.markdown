---
layout: post
title:  "React Intro"
---

Why am I trying React?? I had a bunch of data coming back from Wikipedia API calls and could see how manually building the tables was going to get real old real fast. I decided to see how React/Typescript handle this.

First I went through this [React/GithubPages tutorial](https://github.com/gitname/react-gh-pages).

This was astonishingly easy. Within an hour I had my first React App compiled and running through Github Pages. 

The biggest thing for me to remember from this is this terminal command:

`npm run deploy -- -m "Deploy React app to GitHub Pages"`

Once I had this running, my impules was to jump right into blogs and Stackoverflow threads about how to call the Wikipedia Api the typescript way and display the results in tables the React way.

Instead, I went through this 80 minute [React Tutorial for beginners](https://www.youtube.com/watch?v=SqcY0GlETPk) and learned about:

VSCode Extensions:
- Prettify
- VS Code ES7+ React/Redux/React-Native/JS snippets

and the command:
`rafce` (the reason I started this post was to help me remember where I had this written down!)

## 11 days later
I have updated the github pages react app. It now has two custom components. `EditsTable` and `BlocksTable`. Within these, I am calling the same api calls i was calling in [Wikipedia API Exploration]({{ site.url }}/github-pages-with-docker/2023/11/01/wikipedia-api-exploration )

I'm happy I was able to figure it out. Though, as is expected with a brand new project/technology, I feel pretty sloppy with it. The first thing is my App.tsx file looks like this:

```react

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <EditsTable>Edits Table Child</EditsTable>
        <BlocksTable>Blocks Table Title</BlocksTable>

        <Button
          color="danger"
          onClick={() => alert('Button clicked!!!')}
        >
          We're gonna need a bigger boat
        </Button>
```

Nevermind the obvious experiment button code. That's an easy clean up. The next thing I need to figure out is what a clean code structure is. Right now I'm just rendering table components on the App.tsx page and I have bigger plans for this. 

What I would like is to have each of these components display on their own pages. That is my next modest goal.