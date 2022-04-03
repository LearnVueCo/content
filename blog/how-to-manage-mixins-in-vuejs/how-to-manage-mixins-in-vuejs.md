---
author: Matt Maribojoc
title: How to Manage Vue Mixins
snippet: When your Vue project starts to grow you might find yourself copying and pasting the same data methods and watchers over and over again if you have similar…
createdDate: 2019/12/17
tags: basics,getting started,mixins,vue2
category: Full Tutorials
---

When your Vue project starts to grow, you might find yourself copying and pasting the **same** data, methods, and [watchers](https://learnvue.co/2019/12/a-simple-vue-watcher-tutorial-for-beginners/) over and over again if you have similar components.

Sure — you could write all of these separate files as a single component and use props to customize them.

However, using that many props can easily get **confusing and cluttered**.

To avoid this daunting task, most people just continue adding duplicate code. The best Vue developers will know that there is a better solution – Vue Mixins.

## The Solution – VueJS Mixins

Thankfully, the VueJS gods blessed us with Mixins — one of the easiest ways to share **reusable** code between different components. Mixin objects can use **any of the component options** — data, mounted, created, update, etc — and when a component uses a mixin, all of the information in the mixin object will be, well, mixed in to the component. Then, the component has access to all of the options in the mixin as if you declared it in the component itself. This will make a lot more sense after an example.

```vue
<script>
export default {
    data() {
        return {
            msg: 'Hello World',
        }
    },
    created: function () {
        console.log('Printing from the Mixin')
    },
    methods: {
        displayMessage: function () {
            console.log('Now printing from a mixin function')
        },
    },
}
</script>
```

```js{}[main.js]
import mixin from "./mixin.js";
new Vue({
  mixins: [mixin],
  created: function () {
    console.log(this.$data);
    this.displayMessage();
  },
});
// EXPECTED OUTPUT
// => "Printing from the Mixin"
// => {msg: ‘Hello World’}
// => "Now printing from a mixin function"
```

As you can see, after using the mixin, the component contains all of the data in the mixin, and it is accessed by using `this`*. *You can also define the mixin using a **variable** instead of a separate file.

Honestly, that’s most of what you need to know about mixins. But I think it’s useful to know more about certain use cases and corner cases.

Also, it’s important to note that when using [VueJS lifecycle](https://learnvue.co/2019/12/a-beginners-guide-to-vuejs-lifecycle-hooks/) hooks, the mixin hook will be called before your component’s hook.

## What happens if there’s a naming conflict?

A naming **conflict** between a component and its mixin can happen when there is data, methods, or any component options in the mixin that has the same name as an option in the component.

If this occurs, the property in the **component itself** will take precedence.

For example, if there is a `title` data variable in both the component and mixin — `this.title` would return the value defined in the component. In code, this looks like:

```vue
<script>
export default {
    data() {
        title: 'Mixin'
    },
}
</script>
```

```vue
<script>
import mixin from './mixin.js'
export default {
   mixins: [mixin],
   data () {
      title: ‘Component’
   },
   created: function () {
      console.log(this.title)
   }
}
// Output: "Component"
</script>
```

As you can see, the data from the internal component took precedence over the default mixin value.

## You’re done! Er, well… for now.

As with everything, there’s always more to VueJS Mixins that you can learn. But this should be enough to get you started and covers a **majority** of use cases. There are more **advanced** topics such as global mixins and custom merge setups in Vue. As always, this information is available in their [documentation for Mixins](https://vuejs.org/v2/guide/mixins.html). I love the Vue documentation, the Vue team did a great job making it easy to understand and follow.

Happy Mixing!
