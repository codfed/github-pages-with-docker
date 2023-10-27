---
layout: post
title:  "Creating favicon using Generative AI"
---

![default favicon]({{ site.url }}/github-pages-with-docker/assets/images/favicon-tab-default.png)

Some say that not having a favicon is worthy of harsh judgement. I say it's just a missed opportunity. I've re-learned rudimentary Photoshop skills numerous times over the years in order to craft a killer favicon. 

I am once again presented with this opportunity. Last time I made a favicon I hemmed and hawed about reactivating my Adobe CS license. Before that I would willfully spend hours venturing deep into file structures, disabling my network card, and listening to unmutable music from keygens all to have Photoshop work for free for a few weeks. 

### *This time... I have 15 Dall-E credits*
---
**Prompt**

`I am a software engineer building my own blog site. Please generate a favicon for this site with my initials: CF`

**Results**
![prompt 1 result]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-1.png)

Yeah... ok maybe I need to explain a Favicon better. ChatGPT tells me that favicons are usually 16x16 or 32x32 so let's tighten this prompt up.
---
**Prompt**

`Generate a 32x32 pixel favicon with my initials 'CF' using a muted color scheme`

**Results**
![prompt 2 result]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-2.png)

This is much more like it! Though I'm curious about what it thinks a pixel is... In looking at this, it looks as though they could be large 32x32 pixels with each pixel being a really big pixel. But that fourth result with the grid... the grid has 17 rows so that's just baffling.

---
\
I was so focused on trying to make sense of how many pixels are in a pixel that I almost didn't realize that the second one is fairly favicon-y. Let's see how it looks in a tab.

![favicon version 1]({{ site.url }}/github-pages-with-docker/assets/images/favicon-tab-1.png)

I could call that good enough and push it. But I wanna keep going. Here's what i like:
- The color fluctuation on the left that makes it look like it's being lit from the top left
- The letters filling the entire thing (accomplished post-generation from my crop)

What I'd like to improve:
- Have it be more distinguisable

---
**Prompt**

`Generate a 32x32 pixel favicon with my initials 'CF'. Make sure most of the image is filled with my initials. Use vibrant colors and make a cool gradient effect`

**Results**

![favicon version 3]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-3.png)

I really like the second one. It's the same color pallet of my roller skates and it is a little abstract. I wish the C and F blended together more. And it's actually hard for me to not fire up GIMP and make it my own but... let's keep going.

---
This time let's try to make it more abstract and tongue-in-cheek referencey

**Prompt**

`Generate a 32x32 pixel favicon with my initials 'CF'. Make sure most of the image is filled with my initials. Stylize it as though it is the Wu-Tang Clan logo`

**Results**

![favicon version 4]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-4.png)

I see what you're doing there! Let's try something new.

---

**Prompt**

`I am a software engineer looking to re-brand my personal portfolio. Generate a 32x32 pixel favicon with my initials 'CF'. Make sure most of the image is filled with my initials. Make my initials look like flexing arms.`

**Results**

![favicon version 5]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-5.png)

Is it just me or did this get a lot more boring? Maybe I should remove that software engineer part.

---

**Prompt**

`I am a creative type looking to re-brand my personal portfolio. Generate a 32x32 pixel favicon with my initials 'CF'. Make sure most of the image is filled with my initials. Make my initials look like flexing arms.`

**Results**

![favicon version 6]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-6.png)

Damn... the only difference there was changing 'software engineer' -> 'creative type'. It really cleaned things up and that third one is worth checking out how it looks in a tab.

![favicon version 2]({{ site.url }}/github-pages-with-docker/assets/images/favicon-tab-2.png)

That's not gonna work. Too busy.

---

**Prompt**

`I am a creative type looking to re-brand my personal portfolio. Generate a minimalist 32x32 pixel favicon with my initials 'CF'. Make sure most of the image is filled with my initials. Make my the top right end of both the c and the f look like a thumbs up`

**Results**

![favicon version 7]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-7.png)

These are going down hill. They were a lot better before I was saying I was a software engineer or creative type. I'm gonna remove that and be more direct.
---

**Prompt**

`I need an image that will look good at the small scale of 32 pixels x 32 pixels. It needs to depict 'CF', contain 2 colors, and have slight embellishments on one line of each letter.`

**Results**

![favicon version 8]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-8.png)

I like these more. Not in love with the colors though.

---

**Prompt**

`I need an image that will look good at the small scale of 32 pixels x 32 pixels. It needs to depict 'CF', contain 2 colors in the pastel color pallet, and have slight embellishments on one line of each letter.`

**Results**

![favicon version 9]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-9.png)

I'm in like with these. I could even see going with a few of em but I have 6 Dall-E credits left so I'm going to keep going. It's ignoring the pixels thing, which probably isn't that important in the first place. Gonna switch it up.

---

**Prompt**

`A simple pastel stained glass window with the letters CF`

**Results**

![favicon version 10]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-10.png)

Meh...

---

**Prompt**

`Simple cartoon depiction of two of those old wooden block toys with the letters C on one and F on the other`

**Results**

![favicon version 11]({{ site.url }}/github-pages-with-docker/assets/images/favicon-generation-11.png)

Do we have a winner???

![favicon version 3]({{ site.url }}/github-pages-with-docker/assets/images/favicon-tab-3.png)

## We have a winner!!!! 

### PUSH IT!

Still have 4 credits to spare, no less.

**Prompt**

`The Song of Victory painting except the guy holding the flag is Michael Cera wearing Bean Boots that go all the way up to his thighs`

![favicon celebration]({{ site.url }}/github-pages-with-docker/assets/images/favicon-celebration.png)

errr.... make that 3 credits