---
author: Matt Maribojoc
title: An Introduction to VueJS Suspense Components
snippet: Suspense components allow our app to render fallback content while waiting for asynchronous components - letting us create a smooth user experience.
createdDate: 2020/01/22
tags: composition api,suspense components,vue3
slug: an-introduction-to-vuejs-suspense-components
videoLink: https://youtube.com/v/2wh4feX5LfU
category: Dev Tips
---

Suspense components are one of the well known features in Vue3. They allow our app to render some fallback content while waiting for asynchronous components – letting us create a smooth user experience.

Thankfully, Suspense components are _extremely_ simple to understand and start using in your components. They don’t even require any additional imports!

By the end of this article, you should know:

-   What Suspense components are

<!-- -->

-   When to use them

<!-- -->

-   How to use them

<!-- -->

Enough talking! Let’s get coding.

## What even are Suspense Components?

Suspense components are used to display fallback content when waiting for some sort of asynchronous component to resolve.

You may be wondering, _“When would we even be using an async component?”_

Honestly, more than you might think. Whenever we want our component to wait until it fetches data (which is usually in an async API call), we can make an asynchronous component using the [Vue3 Composition API](https://learnvue.co/2020/01/4-vue3-composition-api-tips-you-should-know/).

Here are some instances when an async component would be useful:

-   Showing a loading animation before a page loads

<!-- -->

-   Displaying placeholder content

<!-- -->

-   Handling lazy loaded images

<!-- -->

Previously, in Vue2, we would have to use conditions (e.g. `v-if `or `v-else`) to check if our data has been loaded and show fallback content.

But now, Suspense comes built in with Vue3 so we don’t have to worry about tracking when our data is loaded and rendering the corresponding content.

## Okay…so how do we implement Suspense?

In this example, we are going to say that we have an asynchronous `ArticleInfo.vue` component.

Since the focus of this article is Suspense and not the Composition API, won’t go into crazy detail about the details. If you’re interested in a more complete Composition API tutorial, I have one here.

Keeping it short, just know that the setup method can be made asynchronous just like any other method.

For our example, ArticleInfo will have an async `setup` method that load’s user data before returning.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">ArticleInfo.vue</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="0"></precode></div></section>

Then, let’s say we have a `ArticlePost.vue `component that contains our ArticleInfo component.

If we want to display something like “Loading Profile…” while waiting for our component to fetch the data and resolve, we can implement suspense in just three steps.

-   Wrap our async component in a `&lt;template #default&gt;` tag

<!-- -->

-   Add a sibling right next to our async component with the tag `&lt;template #fallback&gt;`

<!-- -->

-   Wrap both components in a `&lt;suspense&gt;` component

<!-- -->

Using slots, the suspense will render the fallback content until the default one is ready to go. Then, it will automatically switch to display our async component.

It would look a little like this.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">ArticlePost.vue</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> markup <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="1"></precode></div></section>

## You can also catch component errors

Another cool feature of Vue, especially when we start using asynchronous components, is that we can catch errors and actually show the user some error message.

Even in Vue2, this was possible using the [errorCaptured](https://vuejs.org/v2/api/#errorCaptured) hook, but in Vue3, it has been renamed to `onErrorCaptured`.

Regardless of what it’s called, this [hook](https://learnvue.co/2019/12/a-beginners-guide-to-vuejs-lifecycle-hooks/) runs when an error from any descendant component is captured. We can use this with Suspense to render an error if something goes wrong.

This is what our above component would look like if we handled an error to display an error message.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">ArticlePost.vue</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="2"></precode></div></section>

## There you have it!

Suspense is just another way that Vue makes it easier for developers to tackle common problems. Instead of having to conditionally render components, we can just use Suspense to take care of things for us.

In my opinion, it’s one of the neatest additions to Vue3.

Now, you should have a little more familiarity with Suspense components in Vue and that you’ve thought of some cool ways to start implementing them into your projects!

If you’d like to know more about the differences between Vue 2 and Vue 3, continue reading here.Or if you’re interested in getting started in the Vue3 Alpha Release.
