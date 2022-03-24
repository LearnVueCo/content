---
author: Matt Maribojoc
title: How and Why to Use Wrapper Components in Vue3
snippet: Wrapper components are insanely useful for making your codebase more organized and more professional.
createdDate: 2020/02/18
tags: best practices,vue3
slug: how-and-why-to-use-wrapper-components-in-vue3
category: Dev Tips
---

**Wrapper components are insanely useful** for making your codebase more organized and more professional.

Generally, a wrapper component is a custom component that modifies a native element or 3rd party library by adding some custom functionality, styles, or anything else really.

By the end of this tutorial, you will…

-   Understand the value of using wrapper components

<!-- -->

-   Know when to use them

<!-- -->

-   Build an example input wrapper component

<!-- -->

Enough talk! Let’s begin.

## Why should we even use wrapper components?

As we were saying, wrapper components are useful for both organizing your code and extending native/external elements.

_Okay…but how does it help our organization??_

For our example, let’s imagine that we are building a wrapper component for the default [text input](https://learnvue.co/2020/01/9-vue-input-libraries-to-power-up-your-forms). Using wrapper components creates a natural inheritance – `Parent Element`\ > `TextInputWrapper`\ > `Input`.

Inside `TextInputWrapper`, we can add custom styles, transitions, and extend the default usage of the input element. If we didn’t have a wrapper, we would have to make all of these edits directly to our input element in EVERY component that uses the fancier input.

A wrapper component gives us a [reusable component](https://learnvue.co/2019/12/building-reusable-components-in-vuejs-tabs/) that we can just import and use as is. Now, if we want to change functionality, we only have to edit one file instead of potentially dozens.

So not only do wrapper components help us to keep our code as DRY as possible, but it also builds a more modular and scalable project. For example, if we wanted multiple types of custom text inputs.

## Alright…let’s actually do it!

Okay, now that we actually know what wrapper components are and how they can be useful, let’s actually build the example we were talking about.

For the text input example that we were talking about earlier, let’s make a wrapper component for the native text input.

This is the component we’re building on top of.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6=""></h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="0"></precode></div></section>

**To make a wrapper in Vue3 is insanely simple**. We just have to understand a propertyof a Vue instance: `$attrs`.

`$attrs` contains all of the non-prop attributes and non-emitted events passed to our component.

In Vue2, if we didn’t explicitly define a prop in our component, it was added to the root of the component’s children. However, if we set the `inheritAttrs` instance property to false, we could override this property and can use the $attrs property to pass data through our wrapper component.

However, now in Vue3, the default binding to the component children no longer happens so there is nothing to override. Plus, a component’s non-emitted event listeners that used to be accessed via the $listeners property are also now included in $attrs.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6=""></h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> vue <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="1"></precode></div></section>

With the basic text input now working, we can add some customization to our wrapper component. Some ways to extend it are adding custom event listeners, different styles, or something a label attribute to label our input.

Great. Our wrapper component is set up! Now, here’s an example of how we could include it into a component.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6=""></h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> markup <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="2"></precode></div></section>

If you really want to go into more depth with how v-model, $attrs, and v-bind work in Vue3, here is a[ great slide deck by Chris Fritz](https://github.com/chrisvfritz/vue-3-trends/blob/master/slides-2019-03-vueconfus.pdf)

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/how-and-why-to-use-wrapper-components-in-vue3-1.png)## What else is possible?

The example we just covered is a really simple usage for wrapper components, but it shows one of the main use cases: wrapping native elements to add more functionality.

It’s also a very great technique for incorporating third party libraries or plugins into your Vue project. It allows you to have more predictable control over the actions of certain elements.

In conclusion, wrapper components, especially in larger projects, are a great way to develop a more reusable, organized, and predictable codebase.

After this quick article, you should know why wrapper components are useful and how to structure them using `v-model`, passing `$attrs`, and passing `$listeners` in Vue3. Hopefully, you learned a thing or two and as always, if you have any questions, let me know!!

Happy coding!
