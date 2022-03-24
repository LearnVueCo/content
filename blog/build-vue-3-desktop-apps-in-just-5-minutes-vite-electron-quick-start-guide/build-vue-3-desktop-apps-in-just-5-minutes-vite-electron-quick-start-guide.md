---
author: Matt Maribojoc
title: Building a Vue 3 Desktop App with Vite and Electron
snippet: Let’s a look at how to build a Vue 3 desktop application from your Vite app with Electron - a framework desktop apps with Javascript.
createdDate: 2021/05/09
tags: desktop apps,electron,vite,vue 3
slug: build-vue-3-desktop-apps-in-just-5-minutes-vite-electron-quick-start-guide
videoLink: https://youtube.com/v/nD-UJRlG91Q
category: Top Tools
---

In this article, we’re going to be taking a look at how to Vue 3 Desktop Project from a Vite app.

To do this, we’re going to be using [Electron](https://www.electronjs.org/) – one of the most popular frameworks for building cross-platform desktop apps with Javascript. So many popular apps are using Electron like VSCode, Slack, Twitch, and a ton more.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/build-vue-3-desktop-apps-in-just-5-minutes-vite-electron-quick-start-guide-1.png)Let’s first take a quick look at what we’re going to be doing in this tutorial..

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/build-vue-3-desktop-apps-in-just-5-minutes-vite-electron-quick-start-guide-2.png)So this is just the Vite starter template BUT it’s in its own dedicated app – not in our browser. That’s a super cool step and a necessary one to build your own desktop apps.

Alright – let’s jump right into the code.

## Creating our Basic Vite App

First, let’s make our Vite app. I’m not going to go into too much detail about how Vite works. If you want to learn more about creating your vue project in Vite, check out our youtube video here.

But basically, let’s go to our terminal and run

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">Building our Vite app!</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> bash <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="0"></precode></div></section>

Alright – let’s first try this out just in our browser.

In our terminal, we can just run a plain old `npm run dev`. get our local host url, and load it up.

Here’s the Vite starter template!

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/build-vue-3-desktop-apps-in-just-5-minutes-vite-electron-quick-start-guide-3.png)Perfect – now it’s time to add Electron to this setup.

## Adding Electron to Our Vite Project

For this quick start guide, we’re going to be loosely following the [Electron’s own quick start guide](https://www.electronjs.org/docs/tutorial/quick-start) from the official documentation – and tweaking it a little bit to work inside our Vite application.

The first thing we have to do is actually install Electron – so let’s head over to the terminal and do that.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">Install Electron</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> bash <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="1"></precode></div></section>

Next, let’s take a quick look at the Electron guide again.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/build-vue-3-desktop-apps-in-just-5-minutes-vite-electron-quick-start-guide-4.png)It says that a simple Electron setup needs a four main files:

-   `package.json` – awesome we already have this

<!-- -->

-   `main.js`

<!-- -->

-   `preloader.js`

<!-- -->

-   `index.html`

<!-- -->

At first, it may seem like we already have our `main.js` and `index.html `files, but those are the ones we need for Vite **NOT the ones we need for Electron**. The Vite files are used to run our Vite app, we need separate Electron files for our app.

`main.js` will create our desktop application and load in `index.html`, which will have our built Vite app.

## Building our Vite App

So first things first, we have to build our Vite app. And since we’re working with Electron, we have to do a little bit of extra configuration.

We want to make sure that when our project is built, that all of its references to the final javascript and css files actually point to the right paths.

Building our Vite project creates a dist folder with the following structure.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/build-vue-3-desktop-apps-in-just-5-minutes-vite-electron-quick-start-guide-5.png)But since our Electron code is in our root directory, we want to set the base for our entire project to be this dist folder. We can do this by using the `path` library and setting the `base` property in our `vite.config.js` file.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">vite.config.js</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="2"></precode></div></section>

Now we can just run `npm run build` in our terminal to create our own dist folder!

Perfect.

## Setting up our Electron main.js

The next step is to create our `main.js` file in our **root directory**.

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/build-vue-3-desktop-apps-in-just-5-minutes-vite-electron-quick-start-guide-6.png)Once it’s created, we can just copy and paste the code from the [Electron quick start guide](https://www.electronjs.org/docs/tutorial/quick-start#create-the-main-script-file)!

**There’s one change we have to make though.**

Where we’re loading our `index.html `file, all we have to do is change that to `dist/index.html` so we’re using the file inside our `dist` folder.

So the final code inside `main.js `will look like this…

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">main.js</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="3"></precode></div></section>

## Making preload.js

Next up, let’s create our `preload.js` file in our root directory and once again, we can use the [quick start code](https://www.electronjs.org/docs/tutorial/quick-start#define-a-preload-script) – but this time we don’t have to change anything.

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">preload.js</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> javascript <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="4"></precode></div></section>

## Modifying package.json

Alright – almost there, the last thing we have to do is make some changes to our `package.json` file so that we can actually run some of our Electron commands.

First, we have to set the `main` property – by default, Electron will look for an `index.js` file in the root directory to start our app, but since our file is called `main.js`, we just have to define that in our `package.json`

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">package.json</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> json <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="5"></precode></div></section>

The final thing we have to do is actually make a way to run Electron, so inside the `scripts` section, let’s make a new script called `electron:start` that runs `electron .`

<section class="relative p-3 overflow-hidden rounded-lg bg-accent mb-8" data-v-0be5e7a6=""><div class="absolute px-2 py-1 text-white transition duration-1000 transform -translate-x-1/2 -translate-y-1/2 rounded opacity-0  left-1/2 top-1/2 bg-primary" style="display:none;" data-v-0be5e7a6=""><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 130.2 130.2" fill="#ffffff" class="inline transition duration-300 icon-root" style="dislay:block;" data-v-2c7fa105="" data-v-0be5e7a6=""><path fill="none" stroke="#fff" stroke-width="12" stroke-linecap="round" stroke-miterlimit="10" d="M100.2 40.2L51.5 88.8 29.8 67.5" class="success-path" data-v-2c7fa105=""></path></svg> Copied </div><div class="flex justify-between border-gray-500 border-b pb-2 mb-3" data-v-0be5e7a6=""><h4 class="text-primary" data-v-0be5e7a6="">package.json</h4><div class="flex items-center text-xs text-gray-400" data-v-0be5e7a6=""> json <button class="ml-4" data-v-0be5e7a6=""><svg height="20" viewBox="-21 -21 682.66669 682.66669" width="20" xmlns="http://www.w3.org/2000/svg" fill="#ffffff" class="fill-gray hover:fill-white transition duration-300 icon-root" data-v-2c7fa105="" data-v-0be5e7a6=""><path d="M565 640H225c-41.36 0-75-33.64-75-75V225c0-41.36 33.64-75 75-75h340c41.36 0 75 33.64 75 75v340c0 41.36-33.64 75-75 75zM225 200c-13.785 0-25 11.215-25 25v340c0 13.785 11.215 25 25 25h340c13.785 0 25-11.215 25-25V225c0-13.785-11.215-25-25-25zM100 440H75c-13.785 0-25-11.215-25-25V75c0-13.785 11.215-25 25-25h340c13.785 0 25 11.215 25 25v23.75h50V75c0-41.36-33.64-75-75-75H75C33.64 0 0 33.64 0 75v340c0 41.36 33.64 75 75 75h25zm0 0" data-v-2c7fa105=""></path></svg></button></div></div><div data-v-0be5e7a6=""><precode language="" precodenum="6"></precode></div></section>

And that’s all of the code to build our basic Electron app.

All we have to do now is go to our terminal and say `npm run electron:start` and…

![](https://dltqhkoxgn1gx.cloudfront.net/img/posts/build-vue-3-desktop-apps-in-just-5-minutes-vite-electron-quick-start-guide-7.png)We have our desktop app! Amazing 🙂

## And that’s it!

Obviously, this is just a quick starter guide to get a basic Electron setup inside of Vite.

If you want to see more Vite + Electron tutorials, let me know in the replies because overall i love to teach what you find interesting. so if enough of you want, maybe ill start a series where we build a large Vue desktop app together.

But until then, happy coding!
