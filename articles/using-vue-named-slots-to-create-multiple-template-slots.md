---
author: Matt Maribojoc
title: Using Vue Named Slots to Create Multiple Template Slots
snippet: Vue slots allow you to inject content from a parent component into a child component. Learn better from videos? Here's our Youtube guide to Vue Slots! Here'
createdAt: 2021/04/27
tags: essentials,named slots,slots,tutorial
slug: using-vue-named-slots-to-create-multiple-template-slots
videoLink: https://youtube.com/v/orGcdmCRCc0
category: Dev Tips
---

Vue slots allow you to inject content from a parent component into a child component.

Here’s the most basic example, whatever we put inside `<slot>` will be the fallback content if we don’t give any slot content from the parent.

```vue{}[ChildComponent.vue]
<template>
  <div>
    <slot> Fallback Content </slot>
  </div>
</template>
```

Then this is the code that will go inside of our parent component…

```vue{}[ParentComponent.vue]
<template>
  <child-component> Override fallback content </child-component>
</template>
```

When compiled, our DOM will look like this…

```html
<div>Override fallback content</div>
```

We can also include any data from the scope of our parent component inside our slot content. So if our component had a data field called title, we can inject it into our child component with this code:

```vue{}[ParentComponent.vue]
<template>
  <child-component> {{ title }} </child-component>
</template>

<script>
  export default {
     data () {
       return {
         title: 'This will be passed to our child component!',
       }
     }
  }
</script>
```

This is just a brief summary of how slots work, for a more in-depth guide on slot, check out [Using Component Slots in VueJS — An Overview](https://learnvue.co/2019/12/using-component-slots-in-vuejs%e2%80%8a-%e2%80%8aan-overview/).

## Why do we need named slots

Named slots are useful when creating a component that requires multiple slots.

For example, let’s say we want to create an `Article.vue` component, we might want separate slots for the header, main content area, and comments.

With three different areas, we need a way to differentiate between them or else when we try to inject content from our parent component, our Vue app will have no clue which slot we’re trying to target.

This is where named slots become super useful.

## How to Use Named Slots

There are two steps to using named slots in Vue:

- Naming our slots from our child component using the `name` attribute
- Providing content to these named slots from our parent component using the `v-slot` directive

By default, when we don’t give our slot an explicit name attribute, like in the examples above, it has the name of `default`.

To give our slot a name, `<slot>` elements have a special `name` attribute, that let us differentiate between multiple slots.

In our `Article.vue` example, we can name our three slots like this.

```vue{}[Article.vue]
<template>
  <div>
    <slot name="title"> Fallback Title </slot>
    <slot name="content"> Fallback Content </slot>
    <slot name="comments"> Fallback Comments </slot>
  </div>
</template>
```

Then, in our parent component, we can specify which slot we want to inject content into using the v-slot directive on a `<template>` element.

So wherever we declare our component with Vue named slots, we can create three `<template>` elements, one for each of our slots.

```vue{}[Parent.vue]
<template>
  <div>
    <child-component>
      <template> Our Title </template>
      <template> Our Content </template>
      <template> Our Comments </template>
    </child-component>
  </div>
</template>
```

If we save and take a look at this, you’ll see that there we still our fallback content

![](unnamed-slots.png)

And that’s because our templates are not currently targeting any of our actual defined slots!

To fix this, using the `v-slot` directive, we’ll pass in the name of each slot like this, making sure that the name **matches exactly** what we declared in our child component.

```vue{}[Parent.vue]
<template>
  <div>
    <child-component>
      <template v-slot:title> Our Title </template>
      <template v-slot:content> Our Content </template>
      <template v-slot:comments> Our Comments </template>
    </child-component>
  </div>
</template>
```

Now, we’ll actually see our content being injected into each of the slots.

![](named-slots.png)

And honestly that’s it! I know, it’s really that easy to use named slots in your code.

## What’s the Point of using Vue Named Slots?

So, as we’ve discussed, named slots can help you use multiple slots. **But why is this even useful for us Vue developers?**

Simply put, it allows us better organize our code for development and also allows us to write more scalable code.

By separating out distinct sections entire their own slots, we can easily see where each part of our final app is being added into the DOM.

Personally, I think the greatest part is that it allows us to use slots over the code, making styling things so much easier. In our example, our `Article.vue` child component only had three slots, but in a real app, the slots would look something more like this so that our component can add CSS styles to each section.

```vue
<template>
  <div>
    <div class="title">
      <h1>
        <slot name="title"> Fallback Title </slot>
      </h1>
    </div>
    <div class="content">
      <p>
        <slot name="content"> Fallback Content </slot>
      </p>
    </div>
    <div class="comments">
      <slot name="comments"> Fallback Comments </slot>
    </div>
  </div>
</template>
```

In this example, it’s much easier to see why we would need multiple slots. Since our injected content is separated from each other by different `<div>`, `<p>`, and DOM elements. It’s impossible to pass all of this information in a single slot.

Here’s an example of what our final components might look like in the browser.

![](example.png)

If we check our DOM, we can see that template using v-slot is properly inserting content in the right places.

![](example-dom.png)

All of this means that if we want to use slots in this component, we’re going to need more than one.

## Conclusion

Alright so that’s all for this quick tutorial on Vue named slots. They are a powerful technique to get used to and will allow you to build more robust, yet very customizable components.

I hope this article helped you get a basic idea of how Vue named slots work. If you have any questions, leave them in the replies down below!
