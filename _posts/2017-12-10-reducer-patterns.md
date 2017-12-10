---
layout: post
title:  "Useful Reducer Patterns"
date:   2017-12-10 10:24:01 -0600
categories: reducers
---

# Useful Reducer Patterns

## Accumulation reducer
can be used for numeric values and strings

```
const reducer = (acc, val) => {
  return acc + val;
};

// numeric
reducer(10, 5); // => 15

// string
const res = reducer('hello ', 'paul'); // => 'hello paul'

// combined with reduce
[1, 2, 3, 4, 5].reduce(reducer, 0); // => 15
['hello ', 'paul ', 'again'].reduce(reducer, '')  // => 'hello paul again'

```

## Object combine reducer
can be used to conbined objects to a new object

```
const objReducer = (acc, obj) => {
  return {
    ...acc,
    ...obj
  }
};

// to be used
const obj1 = {name: 'connie', age: 18};
const obj2 = {height: 'short'};
// pattern 1
objReducer(obj1, obj2);

// pattern 2 - with array
[obj1, obj2].reduce(objReducer, {});

```

## Set reducer
can be used to add values to set

```
const setReducer = (acc, val) => {
  return acc.add(val);
};

// to be used
const mySet = new Set([1, 2, 3, 4]);
setReducer(mySet, 5); // => Set { 1, 2, 3, 4, 5 }
setReducer(mySet, 4); // => no duplicated values so Set { 1, 2, 3, 4 }
```