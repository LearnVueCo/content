---
author: Matt Maribojoc
title: An Introduction to Vue Teleport - A New Feature in Vue3
snippet: One of the new features of Vue 3 is the ability to use Vue Teleport elements to easily create Vue modals and popups by moving HTML around your DOM.
createdDate: 2020/09/03
tags: portals,teleport,vue3
slug: an-introduction-to-vue-teleport-a-new-feature-in-vue3
videoLink: https://youtube.com/v/7gNi7QwYLCwa
category: Dev Tips
---

One of the new features of Vue 3 that has been talked about for a while is the idea of Portals – or ways to move template HTML to different parts of the DOM. Portals, which are a common feature in React, were available in Vue2 under the [portal-vue ](https://github.com/LinusBorg/portal-vue)library.

Now in Vue3, there is native support for this concept using the Teleport feature.

In this tutorial, we’ll cover:

-   The purpose of Teleport

<!-- -->

-   A basic example of Teleport

<!-- -->

-   Some cool code interactions

<!-- -->

Here’s an example of what we’ll be making.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/an-introduction-to-vue-teleport-a-new-feature-in-vue3/-image-0.gif)And this is the DOM using Teleport. As you can see, there is this portal-target div outside of our Vue app where our template code is being “teleported”.

Okay! Let’s just jump right in.

## Purpose of the Teleport

The first thing we have to understand is when/why this Teleport function can come in handy.

When working with larger Vue projects, it becomes important to [organize your codebase in a logical manner](https://learnvue.co/2020/03/extract-and-reuse-logic-in-the-vue-composition-api/). However, when dealing with certain types of components like modals, notifications, or tooltips, the logic for the template HTML may be in a different file than where we would want to render the element.

In fact, a lot of the time, these [elements are much easier to manage](https://learnvue.co/2020/01/12-vuejs-best-practices-for-pro-developers/) when they are handled entirely separately from the DOM of our Vue app. All because handling the positioning, z-index, and styling of nested components can get tricky due to handling the scope of all of its parents.

This is where the Teleport function comes in handy. We can write Template code in the component where it’s logic is located – meaning we can use a component’s data or [props](https://learnvue.co/2020/08/an-introduction-to-vue3-props-a-beginners-guide/). But then render it outside of the scope of our Vue app entirely.

Without using Teleport, we would have to worry about [event propagation](https://learnvue.co/2020/01/a-vue-event-handling-cheatsheet-the-essentials) to pass the logic from a child component up the DOM Tree, but now it’s much simpler.

Let’s look at an example.

## How Vue Teleport works

Let’s say that we have some child component where we want to trigger a notification to pop up. As we were just discussing, it’s simpler if we render this notification in an entirely separate DOM tree than Vue’s root `#app `element.

The first thing we would want to do is go to our index.html and add a `&lt;div&gt;` right before `&lt;/body&gt;`.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">index.html</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> html <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="0"></precode></div></section>

Next, let’s start creating our component that triggers the notification to render. If you’re not familiar with Vue3, definitely check out this Vue3 introduction!

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">VuePortals.vue</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="1"></precode></div></section>

In this snippet, when the button is pressed, a notification will be rendered for 2 seconds. However, our main goal is to use Teleport to get the notification to render outside our Vue app.

As you can see, Teleport has one required attribute – to

The to attribute takes in a valid DOM query string and it can be the:

-   id of an element

<!-- -->

-   class of an element

<!-- -->

-   data selector

<!-- -->

-   a responsive query string

<!-- -->

Since we passed it in `#portal-target`, our Vue app will locate the `#portal-target` div we included in index.html and it will teleport all the code inside the portal and render it inside that div.

This is what our result should be.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/an-introduction-to-vue-teleport-a-new-feature-in-vue3/-image-1.gif)Inspecting the elements and looking at the DOM makes it very clear what’s happening.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/an-introduction-to-vue-teleport-a-new-feature-in-vue3/-image-2.png)Basically, we can use all of the logic from our VuePortals [component](https://learnvue.co/2019/12/using-component-slots-in-vuejs%e2%80%8a-%e2%80%8aan-overview/), but tell our project to render that template code somewhere else!

## Conclusion

And that’s a quick introduction to Vue Teleport. I’ll likely write an in-depth guide to some more advanced use cases in the near future, but this should be a great place to get started working with this cool feature!

For a more in-depth tutorial, definitely check out the [Vue3 documentation](https://v3.vuejs.org/guide/teleport.html).

If you have any questions, just leave a comment 🙂

Happy coding!
