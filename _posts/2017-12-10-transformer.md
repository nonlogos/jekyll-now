
---
layout: post
title:  "Transformer Patterns"
date:   2017-12-10 10:24:01 -0600
categories: reducers
---

# Transformer Patterns

A transformer is a function that takes a value and returns a transformed version of it.

## example

```
const toUpper = str => str.toUpperCase();
const shout = str => `${str}!!`;

// transformer pattern
const scream = str => toUpper(shout(str));

const myString = 'hello';
scream(myString) // => HELLO!!
```