---
author: Matt Maribojoc
title: Everything You Need to Know About Vue v-model
snippet: Vue v-model is a directive that provides two-way data binding between an input and form data or between two components.
createdAt: 2021/01/11
tags: directives,essentials,v-model,vue3
slug: everything-you-need-to-know-about-vue-v-model
videoLink: https://youtube.com/v/ZzmGhQequsM
category: Essentials
---

Vue v-model is a directive that provides two-way data binding between an input and form data or between two components.

It’s a simple concept in Vue development, but the true powers of v-model take some time to understand.

By the end of this tutorial, you’ll know all the different use cases for Vue v-model and learn how to use it in your own projects.

Ready?

Me too. Let’s get coding.

## What is Vue v-model?

As we were just discussing, Vue v-model is a [directive](https://012.vuejs.org/guide/directives.html) that we can use in template code. A directive is a template token that tells Vue how we want to handle our DOM.

In the case of v-model, it tells Vue that we want to create a two-way data binding between a value in our template and a value in our data properties.

A common use case for using v-model is when [designing forms and inputs](https://learnvue.co/2020/01/9-vue-input-libraries-to-power-up-your-forms/). We can use it to have our DOM input elements be able to modify the data in our Vue instance.

Let’s look at a simple example that uses a v-model on a text input.

```vue{}[VueVModel.vue]
<template>
  <div>
    <input type="text" v-model="value" />
    <p>Value: {{ value }}</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        value: 'Hello World'
      }
    }
  }
</script>
```

When we type around in our text input, we’ll see that our data property is changing.

![]($BASE_URL/simple.gif)

Perfect.

### The difference between v-model and v-bind?

A directive that is commonly switched up with v-model is the `v-bind `directive.

The difference between the two is that v-model provides **two-way data binding.**

In our example, this means that if our data changes, our input will too, and if our input changes, our data changes too.

However, **v-bind only binds data one way.**

This is useful when creating a clear single direction data flow in your apps. But you have to be careful when choosing between `v-model` and `v-bind`.

## Modifiers for v-model

Vue provides a couple of modifiers that allow us to change the functionality of our v-model.

Each of these can be added like this and can even be chained together.

```html
<input type="text" v-model.trim.lazy="value" />
```

### .lazy

By default, v-model syncs with the state of the Vue instance (data properties) on every [input event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/input_event). This includes things like gaining/losing focus, being blurred, etc.

The `.lazy `modifier changes our v-model so it only syncs after [change events](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event).

This reduces the number of times our v-model is trying to sync with our Vue instance – and in some cases, can increase performance.

### .number

Often, our inputs will automatically type the input as a String – even if we declare our input to be type number.

One way to ensure that our value is handled as a Number is to use the `.number` modifier.

[According to the Vue docs](https://vuejs.org/v2/guide/forms.html#number), if the input changes and the new value cannot be parsed by `parseFloat()`, then the last valid value of the input is returned instead.

```html
<input type="number" v-model.number="value" />
```

### .trim

Similar to trim methods in most programming languages, the .trim modifier removes leading or trailing whitespace before returning the value.

## Using Vue v-model in custom components

Alright, now that we know the basics of v-model inside of forms/inputs, let’s look at an interesting use for v-model – **creating two-way data binding between components.**

In Vue, data binding has two main steps:

- Passing our data from our parent
- Emitting an event from our child to update the parent instance

Using v-model on a custom component allows us to pass a prop and handle an event with just one directive.

```markup
<custom-text-input v-model="value" />

<!-- IS THE SAME AS -->

<custom-text-input
   :modelValue="value"
   @update:modelValue="value = $event"
/>
```

### Alright…what does this even mean?

Let’s continue with our example of using v-model for forms, and use a custom text input called `CustomTextInput.vue`.

The default name for a value passed using v-model is `modelValue` – which is what we’ll be using for our example.

However, we can pass a custom model name like this.

```markup
<!-- We can name v-model, but for our example leave unnamed. -->
<custom-text-input v-model:name="value" />
```

Note: when we use a custom model name, the name of the emitted method will be `update:name`

Here’s a handy graphic from the Vue docs to summarize it.

${BASE*URL}/(https://v3.vuejs.org.ua/images/v-bind-instead-of-sync.png)
*[Source](https://vuejs.org/)\_

### Using v-model from our custom component

We have our parent component setup, so let’s access it from our child component.

There are two things we have to do inside `CustomTextInput.vue`:

- Accept our v-model value as a prop
- Emit an update event when our input changes

Okay – let’s first declare it as a prop inside our script.

```js
export default {
  props: {
    modelValue: String,
  },
}
```

Next, let’s create our template to set the value as your `modelValue` prop and whenever there’s an input event, we emit the new value via `update:modelValue`.

```vue
<template>
  <div>
    <label> First Name </label>
    <input
      type="text"
      placeholder="Input"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </div>
</template>
```

Now, if we go back and look at our code, we can see it in action.

![]($BASE_URL/custom-component.gif)

## Tips for using v-model

Alright!

We’ve covered a basic example of using v-model to bind data between two components.

Let’s take a look at some more advanced ways to use the v-model directive.

### Using v-model multiple times for one component

v-model is not limited to just one use per component.

To use v-model multiple times we just have to be sure to name each prop uniquely and access it correctly inside our child component.

Let’s add a second v-model to our input called `lastName`.

Inside our parent component…

```vue{}[VueVModel.vue]
<template>
  <div>
    <custom-text-input
      v-model='value'
      v-model:lastName='lastName'
    />
    <p> Value: {{ value }} </p>
    <p> Last Name: {{ lastName }} </p>
  </div>
</template>

<script>
import CustomTextInput from './CustomTextInput.vue'

export default {
  components: {
    CustomTextInput,
  },
  data() {
    return {
      value: 'Matt',
      lastName: 'Maribojoc'
    }
  }
}
</script>
```

Then, inside our child component

```vue{}[CustomTextInput.vue]
<template>
  <div>
    <label> First Name </label>
    <input
      type='text'
      :value='modelValue'
      placeholder='Input'
      @input='$emit("update:modelValue", $event.target.value)'
    />
    <label> Last Name </label>
    <input
      type='text'
      :value='lastName'
      placeholder='Input'
      @input='$emit("update:lastName", $event.target.value)'
    />
  </div>
</template>

<script>
export default {
  props: {
    lastName: String,
    modelValue: String,
  }
}
</script>
```

If we go look at our project, we can see both v-model’s working independently.

![]($BASE_URL/multiple-v-model.gif)

### Custom modifiers for our v-model

As we’ve discussed, there are a few modifiers built into Vue. But there will come a time when we’re going to want to add our own.

Let’s say we want to create a modifier that removes all spaces from our input. We’ll call it `no-whitespace`

```markup
<custom-text-input
  v-model.no-whitespace='value'
  v-model:lastName='lastName'
/>
```

Inside our input component, we can capture the modifier using the props. The name for custom modifiers is `nameModifiers`

```js
export default {
  props: {
    lastName: String,
    modelValue: String,
    modelModifiers: {
      default: () => ({}),
    },
  },
}
```

Okay – the first thing we want to do is change our `@input` handler to use a custom method. We can call it `emitValue` and it will accept the name of the property being edited as well as the event object.

```markup
<label> First Name </label>
<input
      type='text'
      :value='modelValue'
      placeholder='Input'
      @input='emitValue("modelValue", $event)'
/>
```

In our `emitValue` method, before we call `$emit`, we want to check our modifiers. If our `no-whitespace` modifier is true, we can modify our value before emitting it to the parent.

```js
export default {
  methods: {
    emitValue(propName, evt) {
      let val = evt.target.value
      if (this.modelModifiers['no-whitespace']) {
        val = val.replace(/\s/g, '')
      }
      this.$emit(`update:${propName}`, val)
    },
  },
}
```

Awesome. Let’s look at our application now.

![]($BASE_URL/result.gif)

Whenever our input changes and we have a space, it will be removed in the parent value!

Awesome.

## Conclusion

Hopefully, this guide taught you something new about Vue v-model.

In its base use case like forms and input data, v-model is a really simple concept. However, when we begin to create custom components and work with more complex data, we can really unleash the true power of v-model.

If you have any questions, let me know in the comments down below!

And as always, happy coding 🙂

```

```
