---
author: Matt Maribojoc
title: Using Component Slots in VueJS — An Overview
snippet: Slots are another way in Vue for a component to inject content into a child component. They help pass data from a parent component to a child component.
createdAt: 2019/12/24
tags: reusable,template,vue2
videoLink: https://youtube.com/v/orGcdmCRCc0
category: Vue Essentials
---

Slots are another way in Vue for a component to **inject content** into a child component. This does this using template code.

In terms of final output, slots perform a similar function as props in Vue — getting data from a parent component to a child component. Slots are also helpful at creating reusable code.

However, whereas props pass data values to the component, slots can just pass direct template code. I think that this comes with a few **benefits** depending on the situation:

- Your child component is more **reusable** — you can pass it different components without worrying about a consistent format/data values
- It’s a lot more **flexible** — you don’t always have to fill every value whereas with props, you’d have to worry about checking if values exist using `v-if`
- This may be a personal thing, but I think the child component looks a lot more **readable**

I think the best way to wrap your head around slots is to just see an example of how to use them and what actually happens.

### The Simplest Use Case

Starting off with slots is a typical use case in which we simply declare a `slot` in the child component and inject content using the parent component.

Let’s check it out. First, let’s setup a parent component called `MyContainer.vue`

```vue{}[MyContainer.vue]
<template>
    <div>
        <my-button>Click Me!</my-button>
    </div>
</template>
```

Next, let’s setup a child component `MyButton.vue` component.

```vue{}[MyButton.vue]
<template>
   <div>
     <slot></slot>
   </div>
</template>
```

When, MyButton.vue renders, the `<slot>` will be **replaced** by `Click Me!` — the content from the parent.

You can pass **any sort of template** from the parent component, it doesn’t have to be just text. It can be a Font Awesome icon, image, or even another component.

### Need Multiple Slots? Name ‘Em!

The best way to organize a slot-based component system is to **name** your slots. This way you can make sure you’re injecting content into the right part of your component.

As you would expect, this is done by adding a **name attribute** to the `slot` in your child component. Then, to add content from the parent, you simply have to make another `<template>` element and pass the name in an attribute called `v-slot`

Let’s see this in action.

```vue{}[BoxElement.vue]
<template>
    <div>
        <slot name="header"></slot>
        <slot name="content"></slot>
    </div>
</template>
```

Then a parent component.

```vue
<template>
  <div>
    <box-element>
      <template v-slot:header>
        This will be injected as the header slot.
      </template>
      <template v-slot:content>
        This will be the content of the element
      </template>
    </box-element>
  </div>
</template>
```

Note: if a slot is not named. It will just have the name of `default`

### Passing Data Scoped Slots

Another neat thing about slots is that you can give the parent component **scoped access** to data inside the child.

For example, if the child component is using a data object to determine what it displays, we can make that data** visible to the parent **and use that while we pass our injected content.

Once again, let’s just check out an example.

If we have this article header slot inside a child component `Article.vue`— in this case, our fallback data is the article title.

```vue{}[Article.vue]
<template>
<div>
   <slot name='header'>
      {{article.title}}
   </slot>
</div>
</template>
```

Now let’s move on to the parent component. What happens if we want to change the content to show the article’s description instead? We wouldn’t be able to do this because our parent component **does not have access** to the the article object inside its child, `Article.vue`

Thankfully, Vue can handle this situation pretty easily. We can bind data from the child slot to the parent template with a simple` v-bind`

Let’s look at our modified div.

```vue{}[Article.vue]
<template>
<div>
   <slot name='header' v-bind:article='article'>
      {{article.title}}
   </slot>
</div>
</template>
```

There. Our parent component has access to this attribute. Now, let’s see how to access it.

Similar to when passing data to a component using props, our child component passes a **props object** with all of the bounded attributes as children.

All we have to do is name this object in our template and then we can access them. We’ll name it `articleInfo` for now, but this is just a variable so you can use anything your heart desires.

```vue{}[ParentComponent.vue]
<template>
<div>
   <article v-slot:header='articleInfo'>
      <!-- we have access to the article object now! -->
      {{ articleInfo.article header }}
   </article>
</div>
</template>
```

Easy right?

### Using Slots to Make Components More Flexible

Props are a great way to reuse components, but they have their limitations depending on your use case. Props tend to work best in components that have the **same format and content**, but just different values.

Sometimes you need to make your components a little more **flexible** and adaptible: maybe you want some components to have certain sections while depending on the what page it’s on, you want to remove other sections.

By injecting your content using slots, it makes it easier to switch around the content of a component without having to worry about using template logic like `v-if` and `v-else` to handle rendering.

### That’s All Folks

I hope this little article helped teach you a thing or two about the possibilities of using slots to organize your Vue projects.

As always, for more information and to get into the more technical details, check out the [Vue documentation](https://vuejs.org/v2/guide/components-slots.html).

Happy Coding!
