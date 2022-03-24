---
author: Matt Maribojoc
title: A First Look at Vue Router in Vue3
snippet: Managing routes is an essential feature for most SPAs. With the new Vue Router in alpha stages we can already start seeing how it works in Vue3.
createdDate: 2020/04/06
tags: essentials,tutorial,vue router,vue3
slug: a-first-look-at-vue-router-in-vue3
category: Essentials
---

**Managing routes is an essential **feature for most single page applications. With the new version of Vue Router in alpha stages, we can already start checking out how it works in the next version of Vue.

A lot of the changes in Vue3 will slightly modify the way we access plugins and libraries, and this includes [Vue Router](https://router.vuejs.org/).

We’ll be taking a look at using the [alpha version Vue Router](https://github.com/vuejs/vue-router-next) in conjunction with the current Vue3 Alpha release.

By the end of this article, you should know how to add Vue Router to your Vue3 projects and have a nice little example going!

## Setting things up

So to start off, we’re going to be using the [Vue3 Webpack preview ](https://github.com/vuejs/vue-next-webpack-preview/)posted by Evan You.

Let’s clone the repo with `git clone https://github.com/vuejs/vue-next-webpack-preview.git`

Then, to add the vue-router alpha to our project, we want to modify our package.json file.

Inside our dependencies, we want to add the following version of vue-router

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6=""></h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> json <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="0"></precode></div></section>

Now, we can finally run `npm install` from our command line to install all of our dependencies.

The final setup we want to do is to actually create our router file and some views for it to map to.

Inside our `src/ `folder, we’re going to add three files.

-   router/index.js

<!-- -->

-   views/Home.vue

<!-- -->

-   views/Contact.vue

<!-- -->

Our router file will – you guessed it – contain our router and our Home/Contact views will just output a single word so we can see what’s happening.

## Creating our routes

Okay – with everything ready to go, let’s start using Vue Router!

Simply put, the main difference in the Vue3 version of vue router is that we have to import new methods in order to get our code working. The most important of which are `createRouter` and `createWebHistory`.

Inside our router/index.js file, let’s import these two methods and our two views from earlier.

Next, what we want to do is create a routerHistory object using the createWebHistory method like this.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">router/index.js</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="1"></precode></div></section>

Before, we could just say `mode: history` to switch from hash to history mode, but now it’s we do that using `history: createWebHistory()`

Next, we can actually create our router using `createRouter`. It accepts an object and we want to pass our `routerHistory` variable as well as an array of our two routes.

And finally, let’s just make our file export our router.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6=""></h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="2"></precode></div></section>

As you can see, from a high level, [it’s still pretty similar to Vue2](https://learnvue.co/2020/02/building-the-same-component-in-vue2-vs-vue3). But with all these changes allowing for better Typescript support and optimizations, it’s good to get familiar with the new methods.

## Making our app use vue router

Now that our Vue Router file is actually set up, we can add it into our project. Previously, we could just import it and say `Vue.use(router)`, but this is different in Vue3.

This is actually a great intro to how we create and mount our Vue application.

Inside our main.js file, you’ll see that we’re using a `createApp` method from Vue to actually create our project. In the default project, it’s chaining the createApp and `mount` methods.

What we want to do is separate these methods like this.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">main.js</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="3"></precode></div></section>

Then, before we mount our app, we want to tell it to use our router file.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6=""></h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="4"></precode></div></section>

Finally, inside our App.vue file, let’s actually display our `router-view` and provide some `router-links` so that we can navigate around.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">App.vue</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="5"></precode></div></section>

So now, if we click around, we’ll see that we can actually navigate between our two pages!

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/a-first-look-at-vue-router-in-vue3-1.gif)BUT if we try to go directly to our` /contact` route it doesn’t work! We get some sort of error.

Luckily this is a really quick webpack fix.

Inside our webpack.config.js file, we want to enable our devServer to use the history api by changing our configuration so it looks like this.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">webpack.config.js</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> json <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="6"></precode></div></section>

Now, if we navigate straight to our Contact route, everything should work properly 🙂

## Conclusion

We’re all done – we’ve successfully added vue-router into our Vue3 project. Most of the other features like navigation guards, handling scrolls, and such work mostly the same.

[Here’s a link to the final Github repo](https://github.com/matthewmaribojoc/vue3-router-template) from this tutorial. It’s a great template code if you want to have vue-router in your Vue3 testing area.

Once all of Vue3 is officially released, I’ll definitely write a more in-depth guide, but knowing how to add it is already a great way to start playing around in the new framework.

I hope you learned a thing or two and are as excited as me to start trying out some of the new features in Vue3.

Happy coding!
