---
author: Matt Maribojoc
title: When/Why to Use Vue Scoped Slots
snippet: Vue slots are a fantastic way to inject content from a parent component into a child component. Learn better from videos? Check out full Youtube video to Vue…
createdAt: 2021/03/29
tags: essentials,scoped slots,slots,vue 3
slug: when-why-to-use-vue-scoped-slots
videoLink: https://youtube.com/v/orGcdmCRCc0
category: Essentials
---

Vue slots are a fantastic way to inject content from a parent component into a child component.

Here’s the most basic example, whatever we put inside `<slot>` will be the fallback content if we don’t give any slot content from the parent.

```vue
<template>
  <div>
    <slot> Fallback Content </slot>
  </div>
</template>
```

And then in our parent component…

```vue
<template>
  <child-component> Override fallback content </child-component>
</template>
```

When compiled, our DOM will look something like this.

```html
<div>Override fallback content</div>
```

We can also include any data from our parent scope inside our slot content. So if our component had a data field called name, we can easily add it like this.

```vue
<template>
  <child-component> {{ text }} </child-component>
</template>

<script>
export default {
  data() {
    return {
      text: 'hello world',
    }
  },
}
</script>
```

This is just a brief overview, for a more in-depth guide on slot, check out [Using Component Slots in VueJS — An Overview](https://learnvue.co/2019/12/using-component-slots-in-vuejs%e2%80%8a-%e2%80%8aan-overview/).

## Why do we need scoped slots

Let’s take a look at another example, say we have an `ArticleHeader` component that contains some article info in its component data.

```vue{}[ArticleHeader.vue]
<template>
  <div>
    <slot v-bind:info="info"> {{ info.title }} </slot>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        info: {
          title: 'title',
          description: 'description',
        },
      }
    },
  }
</script>
```

If we take a closer look at the slot, we’ll see that the fallback content renders the `info.title` of our article.

Without changing the default fallback content, we can easily implement this component like this.

```vue{}[ParentComponent.vue]
<template>
  <div>
    <article-header />
  </div>
</template>
```

And if we look in our browser, our app will be showing the title.

![]($BASE_URL/ex-1.png)

While we could easily change the content of our slot by adding a template expression into our slot, what happens if we want to render the `info.description` from our child component.

It may seem like all you have to do is add it into our slot..

```vue{}[ParentComponent.vue]
<template>
  <div>
    <article-header>
        {{ info.description }}
    </article-header>
  </div>
</template>
```

But if we run this, we get an error: _TypeError: Cannot read property ‘description’ of undefined_

**And that’s because our parent component has no clue what this info object is.**

So how do we solve this?

## Introducing scoped slots!

Simply put, **scoped slots allow our slot content in our parent component to have access to data that’s only found in the child component.** For example, we can use a scoped slot to give our parent component access to `info`.

There are two steps we need to do this:

- Make info available to the slot content using `v-bind`
- Use `v-slot` in our parent scope to access the slot props.

First, to make info available to the parent, we can bind our info object as an attribute on our slot. These bounded attributes are called **slot props**.

The code for that is as easy as this.

```vue{}[ArticleHeader.vue]
<template>
    <div>
        <slot v-bind:info="info"> {{ info.title }} </slot>
    </div>
</template>
```

Then, in our parent component, we can access all of our slot props using `<template>` together with the [v-slot directive.](https://vuejs.org/v2/guide/components-slots.html)

```vue{}[ParentComponent.vue]]
<template>
    <div>
        <child-component>
            <template v-slot="article"> </template>
        </child-component>
    </div>
</template>
```

Now, all of our slot props, which for our example, is only info will be available as a property on our article object, and we can easily change our slot to show our description.

```vue{}[ParentComponent.vue]
<template>
    <div>
        <child-component>
            <template v-slot="article">
                {{ article.info.description }}
            </template>
        </child-component>
    </div>
</template>
```

Our final product will then look like this.

![]($BASE_URL/result.png)

Awesome!

## Conclusion

While Vue scoped slots are a pretty simple concept – give your slot content access to your child component data – it’s super powerful in designing amazing components. By keeping data in one spot and binding it to other places, managing different states becomes much clearer.

I hope this article helped you get a basic idea of how Vue scoped slots work. If you have any questions, leave them in the replies down below!
