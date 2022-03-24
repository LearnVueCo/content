---
author: Matt Maribojoc
title: 7 Simple VueJS Tips You Can Use to Become a Better Developer
snippet: While trying to become better and better at writing VueJS code I’ve come across some tips and tricks that I wish I realized much earlier.
createdDate: 2020/01/08
tags: best practices,efficiency,tips
category: Dev Tips
---

If you’re like me, you started Vue out of curiosity. Personally, I loved it – wanting to learn as much as I could.

While trying to become better and better at writing VueJS code, I’ve come across some tips and tricks that I wish I realized much earlier.

So let’s dive right into these 7 VueJS Tips You Should Know.

Let’s go!

## 1\. Use one component in multiple routes

It’s a pretty common situation developers encounter where multiple routes resolve to the same Vue component.

However, the problem is that Vue optimizes your app and reuses existing components instead of creating new ones. So if you try to switch between routes that use the same component, nothing will change.

```js
const routes = [
    {
        path: '/a',
        component: MyComponent,
    },
    {
        path: '/b',
        component: MyComponent,
    },
]
```

To fix this, you will need to add a :key property onto your <router-view> element – which is likely in your App.vue file. This will help your router recognize when the page is different.

```markup
<router-view :key='$route.path' />
```

Now, your app will not reuse existing components and will update your content when you switch routes.

## 2\. The $on(‘hook:’) can help simplify your code

Removing event listeners is a common Javascript best practice because it helps avoid memory leaks and prevent event collisions.

When adding/deleting component event listeners in Vue, we use the lifecycle hooks mounted and beforeDestroy, respectively. Here’s a typical setup.

```js
export default {
    mounted() {
        window.addEventListener('resize', this.resizeHandler)
    },
    beforeDestroy() {
        window.removeEventListener('resize', this.resizeHandler)
    },
}
```

In the typical pattern, we would have to declare these hooks separately in the component options object. One problem with this is that with larger components, these options can be hundreds of lines apart.

However, looking at the Vue docs, we see that there is an instance method $on that listens for instance events. Also, [VueJS lifecycle hooks](https://learnvue.co/2019/12/a-beginners-guide-to-vuejs-lifecycle-hooks/) emit custom events whenever they are triggered. The event name is the “hook:” + name of the hook itself (e.g. hook:created)

Combining these two tips allows us to write the code for both adding and removing inside just the mounted method. The code would look something like this.

```vue
<script>
mounted () {
    window.addEventListener('resize', this.resizeHandler);
    this.$on("hook:beforeDestroy", () => {
      window.removeEventListener('resize', this.resizeHandler);
    })
}
</script>
```

This means we don’t have to define another lifecycle hook. Something that can greatly increase code readability.

## 3\. $on can also listen to a child component’s lifecycle hooks

Going off the last tip, the fact that lifecycle hooks emit custom events means that parent components can listen to its childrens’ lifecycle hooks.

It would use the normal pattern for listening to events (@event) and can be handled just like other custom events.

```markup
<child-comp @hook:mounted="someFunction" />
```

## 4\. Use immediate: true to trigger watchers on initialization

[Vue Watchers](https://learnvue.co/2019/12/a-simple-vue-watcher-tutorial-for-beginners/) are a great way to add advanced functionality (API calls for example) that runs whenever an observed value changes.

However, by default, watchers don’t run on initialization. Depending on your function, this could mean that some data does not completely initialize.

```js
export default {
    watch: {
        title: (newTitle, oldTitle) => {
            console.log('Title changed from ' + oldTitle + ' to ' + newTitle)
        },
    },
}
```

If you need your watchers to run as soon when an instance is initialized, all you have to do is to convert your watcher into an object that has a `handler (newVal, oldVal)` function and also a immediate: true property.

The code for that might look like this.

```js
export default {
    watch: {
        title: {
            immediate: true,
            handler(newTitle, oldTitle) {
                console.log(
                    'Title changed from ' + oldTitle + ' to ' + newTitle
                )
            },
        },
    },
}
```

## 5\. You should **always** validate your props…please.

Validating props is one of the essential practices in Vue. It’s even listed as a “Priority A: Essential” style rule on the [VueJS official style guide](https://vuejs.org/v2/style-guide/#Prop-definitions-essential).

_Why is it important?_

Well. It basically saves future you from current you. When designing a large scale project, it’s easy to forget exactly the exact format, type, and other conventions you used for a prop.

And if you’re in a larger dev team, your coworkers aren’t mind-readers so make it clear to them how to use your components!

So save everyone the hassle of having to painstakingly trace your component to determine a prop’s formatting and please just write prop validations.

> When designing a large scale project, it’s easy to forget exactly the exact format, type, and other conventions you used for a prop.

Here’s an example of prop validation from the VueJS style guide.

```vue
<script>
props: {
  status: {
    type: String,
    required: true,
    validator: function (value) {
      return [
        'syncing',
        'synced',
        'version-conflict',
        'error'
      ].indexOf(value) !== -1
    }
  }
}
</script>
```

## 6\. Passing all props to a child component is easy

Speaking of props, it’s useful to know how you can pass **all** props from a parent component to one of its children.

There are tons of use cases for this, but it’s especially handy when your project has a very hierarchical structure.

It’s straightforward – you just have to remember your instance properties!

```markup
<child-comp v-bind="$props"></child-comp>
```

## 7\. You HAVE TO understand all the component options

If you really want to become an expert VueJS developer, you need to know all of the different component options, when to use them, and why to use them.

_And you will. Don’t worry._

It just takes time, but after spending more and more time working in VueJS and being dedicated to learning the top tips, best practices, and new methodology, you’ll become a super-dev in no time.

> If you really want to become an expert Vue developer, you need to know all of the different component options, when to use them, and why to use them.A*nd you will. Don’t worry.*

For starters, some questions you should be able to answer are:

-   [How do I choose between a computed property and a watcher?](https://learnvue.co/2019/12/a-simple-vue-watcher-tutorial-for-beginners/)
-   [Which lifecycle hook should I use to make API calls?](https://learnvue.co/2019/12/a-beginners-guide-to-vuejs-lifecycle-hooks/)
-   [When should I use a mixin? What even is that?](https://learnvue.co/2019/12/how-to-manage-mixins-in-vuejs/)

There are thousands of little tricks that help make your code more efficient. But I’m sure if you’re reading this article, you’re interested in learning them!

# Conclusion

This is by no means a comprehensive list of VueJS tips. These are just some of the ones that I personally find the most useful. Some of these tips took me ages of developing in Vue to discover, so I thought I could share that knowledge with all of you.

I hope that you find them as helpful as I do!

What are your favorite VueJS tips and tricks? I’d love to learn from you too!
