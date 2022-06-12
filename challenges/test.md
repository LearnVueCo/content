---
title: V-Model Stackblitz Test
files: App.vue
---

`v-model` tells Vue that we want to create a two-way data binding between a value in our `template` and a value in our `script`.

In this challenge, we want to use `v-model` to display the content of our input inside an h1

::challenges-example

Our `h1` text should match our `input` value.
| input | h1 text |
| ----------- | ------------------ |
| hello | hello |
| hello world | hello world |

::

```vue
<script setup>
import { ref } from 'vue'
</script>

<template>
  <h1>Bind to Input</h1>
  <input />
</template>
```

```js
describe('template basics', () => {
  const AppComponent = __modules__['App.vue'].default

  it('should have an h1   ', () => {
    const wrapper = mount(AppComponent)
    expect(wrapper.find('h1').exists()).toBe(true)
  })
  it('should have an input', () => {
    const wrapper = mount(AppComponent)
    expect(wrapper.find('input').exists()).toBe(true)
  })
  it('typing in input should update our h1', async function () {
    const wrapper = mount(AppComponent)
    const input = wrapper.find('input')
    await input.setValue('does this work?')
    expect(wrapper.find('h1').text()).toEqual('does this work?')
  }, 5000)
})
```
