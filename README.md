# Frontend Mentor - Workit landing page solution

This is a solution to the [Workit landing page challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/workit-landing-page-2fYnyle5lu). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
    - [The challenge](#the-challenge)
    - [Screenshot](#screenshot)
    - [Links](#links)
- [My process](#my-process)
    - [Built with](#built-with)
    - [What I learned](#what-i-learned)
    - [Continued development](#continued-development)
    - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

**Note: Delete this note and update the table of contents based on what sections you keep.**

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the interface depending on their device's screen size
- See hover and focus states for all interactive elements on the page

### Screenshot

![](./screenshot.jpeg)

### Links

- Solution URL: [Frontend Mentor Solution Page](https://www.frontendmentor.io/solutions/supertricky-landingpage-with-multilayered-design-QkxFFZNl0i)
- Live Site URL: [Add live site URL here](https://aleknovkovski.github.io/FEM-workit-landing-page/working/)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox

### What I learned

#### I learned to create multi-layered designs combining ::before and ::after as well as z-index

This challenge involved a pretty tricky effect where you have:
- A section which ends in a divider
- You have an element (the smartphone) that should lay on top of the divider
- And you have these graphical elements in the background which exist in between the section background and the content

Trying to do each of these using a conventional and intuitive method is relatively straightforward. It's combining the 3 at the same time that requires an unconventional approach.

So the solution involved setting an ::after which is at 100% height and width, and then applying (border-radius: 0 0 80% 80%) to get curved bottom. This gives us the divider effect. We also set this one to a z-index of minus-1

You then set the section itself to a z-index of one. So somehow this produces a layered effect where the section content is at z-index(1), and the content of the section::after is at z-index(-1)... yet somehow, the background of section ends BEHIND the content of ::after (as if it were a -2)

In a "graphical sense", the layers end up like so

>SectionBackground | {-2}

>Section::After | (-1)

>SectionContent | (1)

-* By {-2} I mean that it acts as if it were a -2 in depth.

Next, in order to add graphical elements in the section, you create a ::before. Same logic as the ::after; Except we're not setting the z-index on this one, so this will allow it to exist on top of the main section content. In a graphical sense it will act like a 2 in depth, or we get the following:

>SectionBackground | {-2}

>Section::After | (-1)

>SectionContent | (1)

>Section::Before | (2)

Since this will act as if it were a layer on top of the content, we set it to transparent background to make sure the content behind it is visible. We'll only use it to set transparent shapes in the background-image space.

Note also that since this is now a layer covering the content-layer, any clickable stuff inside the content layer becomes unclickable. So we have to add a (pointer-events: none) line to the ::after layer, if we want stuff to be clickable on the content-level layer.

## Author

- Frontend Mentor - [@aleknovkovski](https://www.frontendmentor.io/profile/aleknovkovski)
- Linkedin - [@aleknovkovski](https://www.linkedin.com/in/aleknovkovski/)