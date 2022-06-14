---
author: Matt Maribojoc
title: 7 Ways to Write Better Vue v-for Loops
snippet: In VueJS v-for loops allow you to write for loops in template code. Read six ways to make your v-for code more precise predictable and powerful.
createdAt: 2020/02/25
tags: best practices,dev tips,v-for
videoLink: https://youtube.com/v/G_nwbIAHW10
category: Vue Essentials
---

In Vue, v-for loops are something that every project will use at some point or another. They allow you to write for loops in your template code.

This is awesome for things like…

- Rendering arrays or lists
- Iterating through an objects properties

In its most basic usage, Vue v-for loops are used like this.

```html
<ul>
  <li v-for="product in products">{{ product.name }}</li>
</ul>
```

However, in this article, we’ll be covering some amazing ways to make your v-for code more precise, predictable, and efficient.

Alright – let’s dive right in.

## 1\. Always use keys in Vue v-for loops

To start off, we’ll be discussing [a common best practice](https://learnvue.co/2020/01/12-vuejs-best-practices-for-pro-developers/) most Vue developers already know – **use :key in your v-for loops**. By setting a unique key attribute, it ensures that your component works the way you’d expect.

If we don’t use keys, Vue will try to make the DOM as efficient as possible. This may mean that v-for elements may appear out of order or other unpredictable behavior.

If we have a _unique_ key reference to each element, then we can better predict how exactly the DOM will be manipulated.

```html
<ul>
  <li v-for="product in products" :key="product._id">{{ product.name }}</li>
</ul>
```

## 2\. Using v-for to loop over a range

While most of the time v-for is used to loop over arrays or objects, there are definitely cases where we might just want to **iterate a certain number of times.**

For example, let’s say we are creating a pagination system for an online store and we only want to show 10 products per page. Using a variable to track our current page number, we could handle pagination like this.

```html
<ul>
  <li v-for="index in 10" :key="index">{{ products[page * 10 + index] }}</li>
</ul>
```

## 3\. Avoid use v-if in loops

A super common mistake is to improperly use `v-if `to [filter the data](https://learnvue.co/2020/01/how-to-use-vuejs-filters-to-write-better-code/) that we are looping over with our v-for.

Although this seems intuitive, it causes a huge performance issue – [VueJS prioritizes the v-for over the v-if directive.](https://vuejs.org/v2/style-guide/#Avoid-v-if-with-v-for-essential)

What this means is that your component will loops through every element and THEN checks the v-if conditional to see if it should render.

> If you use v-if with v-for, you’ll be iterating through every item of your array no matter what your conditional is.

```html
<!--BAD-->
<ul>
  <li v-for="product in products" :key="product._id" v-if="product.onSale">
    {{ product.name }}
  </li>
</ul>
```

_So what’s the issue?_

Let’s say our products array has thousands of items, but there only 3 products on sale that we want to render.

**Every time we re-render, Vue will have to loop over thousands of items even if the 3 products on sale did not change at all.**

Try to avoid this.

Let’s look at two alternatives we can use instead of joining `v-for `with `v-if`.

## 4\. Use computed properties or a method instead

To avoid the above problem, we should filter our data _BEFORE_ iterating over it in our template. There are two very similar ways to do this:

- Using a [computed property](https://learnvue.co/2019/12/mastering-computed-properties-in-vuejs/)
- Using a filtering method

The way you choose to do this is up to you, so let’s just cover both real quick.

First, we just have to set up a computed property. To get the same functionality as our earlier v-if, the code would look like this.

```vue
<template>
  <ul>
    <li v-for="products in productsOnSale" :key="product._id">
      {{ product.name }}
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      products: [],
    }
  },
  computed: {
    productsOnSale: function () {
      return this.products.filter((product) => product.onSale)
    },
  },
}
</script>
```

This has a few benefits:

- Our data property will only be re-evaluated when a dependency changes
- Our template **will only loop over the products on sale**, instead of every single product

The code for the method is pretty much the same, but using a method changes how we access the values in our template. However, if we want to be able to pass in a variable to filtering process, methods are the way to go.

```vue
<template>
  <ul>
    <li v-for="products in productsOnSale(50))" :key="product._id">
      {{ product.name }}
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      products: [],
    }
  },
  methods: {
    productsOnSale(maxPrice) {
      return this.products.filter(
        (product) => product.onSale && product.price < maxPrice
      )
    },
  },
}
</script>
```

## 5\. Or surround your loop with a wrapper element

Another time you may want to join v-for with `v-if `is when deciding whether or not to render a list at all.

For example, what if we only want to render our products list when a user is logged in.

```html
<!--BAD-->
<ul>
  <li
    v-for="product in products"
    :key="product._id"
    v-if="isLoggedIn"
    <!--
    HERE
    --
  >
    > {{ product.name }}
  </li>
</ul>
```

_What’s wrong with this?_

Same as before. Our Vue template will prioritize the v-for – so it will loop over every element and check the v-if.

**Even if we end up rendering nothing, we’re going to loop over thousands of elements.**

The easy solution here is to move our `v-if` statement.

```html
<!--GOOD-->
<ul v-if="isLoggedIn">
  <!-- Much better -->
  <li v-for="product in products" :key="product._id">{{ product.name }}</li>
</ul>
```

This is much better because if `isLoggedIn` is false – we’re not going to have to iterate at all.

Awesome.

## 6\. Access the index in your loop

In addition to looping over an array and accessing each element, we can also keep track of the index of each item.

To do this, we have to add an index value after our item. It’s super simple, and is useful for things like pagination, displaying the index of a list, showing rankings, etc.

```markup
<ul>
  <li v-for='(products, index) in products' :key='product._id' >
    Product #{{ index }}: {{ product.name }}
  </li>
</ul>
```

## 7\. Iterating over an object

So far, we’ve only really looked at using v-for to iterate through an array. But we can just as easily iterate over an object’s key-value pairs.

Similar to accessing an element’s index, we have to add another value to our loop. If we loop over an object with a single argument, we’ll be looping over all of the items.

If we add another argument, we’ll get the **items** AND **keys**. And if we add a third, we can also access the **index** of the v-for loop.

With everything, it would look like this.Let’s just say we want to loop over each property in our products.

```markup
<ul>
  <li v-for='(products, index) in products' :key='product._id' >
    <span v-for='(item, key, index) in product' :key='key'>
      {{ item }}
    </span>
  </li>
</ul>
```

## Conclusion

Hopefully, this quick article taught you some of the best practices about using Vue’s v-for directive.

What other tips do you have? Let me know in the replies!!

Happy coding 🙂
