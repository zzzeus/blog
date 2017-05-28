---
title: Some ways to get a word in the TextView (Android)
date: 2017-05-06 20:00:34
tags:
---

## Today I try to make one of my app more interesting.I want to add a function to my app.When I click a word,I can see the definition of the word

I looked and finally find some way to implement it.
* The TextView has a function called getOffsetForPosition(x,y),However it seems not work well.
* We can try to use ClickableSpan in the textview.However I have not do it myself but I think the way is not effective.
* Try to get get the line by y,and get y,which may improve the accuracy.
* Not try to contain all the Strings in one TextView and make TextViews dynamically.

```
//use getOffsetForPosition(x,y)
TextView.getOffsetForPosition(x,y+scrollView.getScrollY());

```
