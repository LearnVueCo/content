---
author: Matt Maribojoc
title: An Introduction to Vue3 Props - A Beginner’s Guide
snippet: The ability to pass data between components is a key part of Vue projects. In Vue3 the way we access props inside components is different than before.
createdDate: 2020/08/25
tags: basics,props,tutorial,vue3
slug: an-introduction-to-vue3-props-a-beginners-guide
category: Essentials
---

Props are an essential part of any modern Javascript framework.

The ability to pass data between components is a fundamental element of Vue projects. In Vue3, the way we can access props inside a Vue component is a little different than before.

In this quick little article, we’ll go over this new change as well as take a look at the decisions behind the switch.

Alright, let’s jump right in!

## Why is it important to use props?

First, we have to understand what [props are.](https://vuejs.org/v2/guide/components-props.html) Props are custom attributes that we can register on a component that allow us to pass data from a parent component to one of its children.

Since props allow us to share data between components, it lets us organize our Vue projects and components into more modular components.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/an-introduction-to-vue3-props-a-beginners-guide-1.png)## Let’s just jump into an example

Previously, a component’s props were just part of the `this` object and could simply be accessed by using this.propName.

However, one huge change in Vue3 is the introduction of the setup method.

This setup method, which you can learn more about here, now contains almost all of the code that used to be separated into different options like data, computed, watchers, etc. One major detail about this new method is that `this` does not have the properties that it used to in Vue2.

So how do we use Vue3 props without using `this`?

Luckily, it’s super simple. Our setup method actually takes two arguments

-   `context` – an object that exposes specific properties that used to be found on `this`

<!-- -->

-   props – an object that contains a component’s `props`

<!-- -->

As you might guess, this props argument is what we’re going to be using to access our props. All we have to do is props.propName – no more need for the this variable!

Our code might look something like this.

<section class="relative p-3 mb-8 overflow-hidden rounded-lg bg-accent" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0 left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6=""></h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="transition duration-300 fill-gray hover:fill-white icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="0"></precode></div></section>

Easy right!

## Why do Vue3 props work differently than Vue2?

The main motivation behind the change in the way we access Vue3 props is to make it clearer `this` means in a component/method. Sometimes when looking at Vue2 code, it could be ambiguous what `this` was referring to.

A big goal for the Vue Team when designing Vue3 was to make it more scalable for large projects. Part of this was redesigning the Options API to the Composition API to allow for better code organization.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/an-introduction-to-vue3-props-a-beginners-guide-2.png)But by eliminating a majority of references to `this` and instead using explicit context and props variables, it would increase readability for large Vue projects.

If you want to learn more about the setup method and the [main differences between Vue2 and Vue3, check out this article](https://learnvue.co/2020/02/building-the-same-component-in-vue2-vs-vue3).

## And there ya go!

As you can tell, Vue3 props work generally the same as Vue2, the main change is how we can access them inside our new setup method.

I hope that this quick little lesson will help make the transition to Vue3 a little bit easier.

If you have any questions, comments, or just want some Vue help, leave a comment down below. Happy coding!
