---
layout: post
title:  "How did we get here?"
date:   2023-10-25 17:10:30 +0000
categories: jekyll github pages docker
---

As a Full Stack Ruby on Rails Engineer, I have been feeling a bit uninspired with my current project. I've been curious about AI so I had been going through the `fast.ai` [Practical deep Learning for Coders course](https://course.fast.ai/).

In the second lesson we learned how to train a model then publish it to huggingface.io. From there you can use an internal UI to access it, or you can access it through an API.

I thought, "cool! I wanna do that and showcase future models on my own website". 

### Let's get a new site!

The only problem with that is I have long since deactivated my sandbox Rails environment hosted in a Digital Ocean droplet. But that's me getting ahead of myself again. What I have in mind does not need a database so github pages will do... right?

It worked when I wanted to play around with `d3.js` 10 years ago with [mapsonmaps.co](http://mapsonmaps.co/d3Thematic.html). Though now it's riddled with DOMExceptions because, as could be expected... browser security rules have changed. *you don't need to fix that right now.you don't need to fix that right now. you don't need to fix that right now. you don't need to fix that right now*

### Github pages revisited

I set up a new github page as a sandbox. I was following a tutorial. Blindly committing new formatting and pages. Gleefully watching the site update... until I wasn't. Until my page looked like this...

<img src="{{ site.url }}/github-pages-with-docker/assets/images/github-pages-error.png" alt="drawing" width="650"/>


Ok, how do I debug this??? I need to figure out how to run it locally. NBD, right? Well, it's not a small deal but the steps are simple if you know what they are. So I found this youtube video [Develop GitHub Pages locally in a Ubuntu Docker Container](https://www.youtube.com/watch?v=zijOXpZzdvs) by [Bill Raymond](https://dev.to/billraymond).

### Develop GitHub Pages locally in a Ubuntu Docker Container
Bill keeps a good balance of detailed, but never lost in the weeds. At least right now, all of the versions play nicely and I got through it with only one or two external queries. 

The only thing I'm unsure of is whether I needed to override the gem-based theme. It added a lot of extra files to my project and I'm not too picky about formatting for this site. BUT it's good to know how to do that if I need to.

### Can't argue with results!
Now I have a github pages site that is running locally with live reload to compose this blog post with!!!

So far the only thing I don't like about Jekyll is/the/long/and/backslash/heavy/urls. But keeping an open mind, maybe those are only annoying at first glance and there's no functional reason why this convention should be different? 

Ok, back to a slightly less open mind... there has to be a better way to access this site than: `...github-pages-with-docker/jekyll/github/pages/docker/2023/10/25/how-did-we-get-here.html`
