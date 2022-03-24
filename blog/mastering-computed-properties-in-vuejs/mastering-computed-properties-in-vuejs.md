---
author: Matt Maribojoc
title: The Guide to Vue JS Computed Properties - Updated 2021
snippet: Vue JS computed properties can help organize code and create reusable data. Learn how to use them!
createdDate: 2019/12/17
tags: basics
slug: mastering-computed-properties-in-vuejs
category: Essentials
---

Vue JS computed properties can be a lifesaver. There are few things more frustrating to a programmer than staring at a block of code and taking years to decipher what’s going on.

When working in VueJS, one of the most common ways to clutter code is to add very long expressions to your template. For example, say we want to render a reversed string, without spaces, and in all caps.

If we were to do this using an in-template expression, it would look like this.

<section class="relative p-3 mb-8 overflow-hidden rounded-lg bg-accent" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0 left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between pb-2 mb-3 border-b border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">ew.</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="transition duration-300 fill-gray hover:fill-white icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="0"></precode></div></section>

Now you may be more of a programming pro than me, but this is way too cluttered for me to look at a glance and know immediately what it’s trying to do.

Now imagine having to use this value in multiple places in a template and having this long expression all over your code.

This is when it’s a lifesaver to use Vue JS computed properties.

## Ok, but how do computed properties work?

Now that we know why Vue JS computed properties are useful, let’s go over how to use them.

In most basic terms, we just add a field to our Javascript exports and define our computed properties there.

For the example above, it would look like this.

<section class="relative p-3 mb-8 overflow-hidden rounded-lg bg-accent" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0 left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between pb-2 mb-3 border-b border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">computed properties in the options api</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="transition duration-300 fill-gray hover:fill-white icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="1"></precode></div></section>

Now that we’ve defined our computed property, it becomes super easy to render it in our template. This is all we have to do.

<section class="relative p-3 mb-8 overflow-hidden rounded-lg bg-accent" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0 left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between pb-2 mb-3 border-b border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">much better.</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="transition duration-300 fill-gray hover:fill-white icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="2"></precode></div></section>

That’s it. Now, on our webpage, we should render `DLROWOLLEH` in a much cleaner and readable way.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/mastering-computed-properties-in-vuejs-1.png)Using computed properties always makes your project more scalable. If we want to change the way the value is computed, we would only have to change **one computed property** instead of potentially hundreds of expression templates.

## So, when exactly does the computed property change?

Since a computed property is like a [more detailed Vue watcher](https://learnvue.co/2019/12/a-simple-vue-watcher-tutorial-for-beginners/), it will observe a piece of reactive data and update when that reactive data changes.

For our example, `formattedText` will always be dependent on the value of text. So if we were to change text to ‘ABCDEF’, then formattedText will return ‘FEDCBA’.

However, in order to run more efficiently,** Vue caches computed property values**.

> Vue JS will only recalculate the property when a reactive dependency is changed.

In our case, it will only recalculate when text changes. Otherwise, it will return the cached value from the last change.

### The Basics of Vue Reactivity

To fully understand when computed properties will change, we have to understand the idea of their reactive dependencies.

Simply put, a computed property’s dependencies are the **reactive** values that help the property that determine the value that is returned. If none of these change, then, again, the cached value will be returned.

If no reactive dependency is changed, a computed property is not recalculated.

The following example from in the [Vue docs](https://vuejs.org/v2/guide/computed.html) shows a computed property that will never recalculate.

<section class="relative p-3 mb-8 overflow-hidden rounded-lg bg-accent" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0 left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between pb-2 mb-3 border-b border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">this will never update.</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="transition duration-300 fill-gray hover:fill-white icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="3"></precode></div></section>

Although the computed property now returns a value that changes _literally_ all the time, there are no dependencies that Vue watches for. Therefore, it is never recomputed.

If you don’t like this, you can always use a regular Vue **method, which by is recalculated on every render**.

<section class="relative p-3 mb-8 overflow-hidden rounded-lg bg-accent" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0 left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between pb-2 mb-3 border-b border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">methods instead of the computed</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="transition duration-300 fill-gray hover:fill-white icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="4"></precode></div></section>

## You can also define a setter for a computed property

By default, computed properties are read only and cannot be set. However, if you want to add a hook for a computed property that allows its dependencies to be set.

All you have to do is the following.

<section class="relative p-3 mb-8 overflow-hidden rounded-lg bg-accent" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0 left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between pb-2 mb-3 border-b border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">computed properties w/ setters!</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="transition duration-300 fill-gray hover:fill-white icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="5"></precode></div></section>

For example, here’s some commands and their impact on the code.

<section class="relative p-3 mb-8 overflow-hidden rounded-lg bg-accent" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0 left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between pb-2 mb-3 border-b border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">expected output</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="transition duration-300 fill-gray hover:fill-white icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="6"></precode></div></section>

## Computed Properties in the Vue 3 Composition API

With the [Vue 3 ](https://learnvue.co/2020/12/setting-up-your-first-vue3-project-vue-3-0-release/)Composition API, the way that we access computed properties is a little bit different.

First, similar to ref and [lifecycle hooks](https://learnvue.co/2020/12/how-to-use-lifecycle-hooks-in-vue3/), we have to import computed into our script.

Then, we can use computed properties in our setup method.

Remember – we have to use `.value` to reference the value of refs!

<section class="relative p-3 mb-8 overflow-hidden rounded-lg bg-accent" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0 left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between pb-2 mb-3 border-b border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">computed properties in the composition api</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="transition duration-300 fill-gray hover:fill-white icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="7"></precode></div></section>

As you can see, the code for the computed property itself is primarily the same, but the setup is different.

## Conclusion

You should have all of the basics to be able to use computed properties. Hopefully, this helps you condense your code and make it more readable and easy to understand.

If you want a more technical and more to the point usage of how exactly computed properties work. Check out the [Vue documentation](https://v3.vuejs.org/guide/introduction.html) for more.

Let me know what tips you have!
