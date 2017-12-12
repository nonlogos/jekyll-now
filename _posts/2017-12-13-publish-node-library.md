---
layout: post
title: How to publish a public or private node library
categories: setup
---

As we enbrace more on microservices at work, I was tasked to build the new order management feature api as a private (public also included) node library. Here is the step by step guide to how to set one up based on a couple tutorials.
<!--more-->

## Set up git repo
1. create a new git repo
2. create a new local folder
3. in your terminal and inside the local folder, run `git init`
4. run `git remote add {url to remote git repo}` to add the remote link to the local repo

## Add manifest file to npm package using npm init
run `npm init` and it will give you a list of questions to set up your package
  1. name: defaults to the folder name. Otherwise you can give it a new name. For private package, add `@` to your namespace
  2. entry point: we are compiling files into a build folder so the path is `build/index.js`

## Set up compilation of source code using babel with npm scripts
compile build script using Babel
1. install babel with `npm install babel-cli babel-preset-latest --save -dev`
2. in package.json add the following script

{% highlight javascript %}
"script": {
  "build": "babel src -d build"
}
"babel": {
  "presets": ["latest"]
}
{% endhighlight %}
3. create a src folder and an index.js file inside.  This is where the source codes will live

## Run builds on file changes using watch with npm scripts
1. install watch with `npm install watch --save -dev`
2. add the following to the package.json scripts
{% highlight javascript %}
"script": {
  "dev": "watch 'npm run build' src'",
  "build": "babel src -d build",
}
"babel": {
  "presets": ["latest"]
}
{% endhighlight %}
3. now, if we run `npm run dev` it will watch and rebuild on any saved file change

## Set up testing of source code using jest with npm scripts
1. install jest with `npm install jest --save -dev`
2. add the following to pacakge.json config
{% highlight javascript %}
"script": {
  "dev": "watch 'npm run build' src'",
  "build": "babel src -d build",
  "test": "jest",
  "test:watch": "npm test -- --watch"
}
"babel": {
  "presets": ["latest"]
}
{% endhighlight %}
3. add new test files with extension xxx.test.js (or create a test folder)
4. run `npm run test` to run the test
5. run `npm run test:watch` to watch for changes and rerun test

## Add package functionality using npm scripts
1. open two terminal tabs
  1. one run `npm run dev`
  2. run `npm run test:watch` on the other
2. develop in the src folder 

## Resources
* [egghead](https://egghead.io/lessons/javascript-add-manifest-files-to-npm-packages-using-npm-init)
