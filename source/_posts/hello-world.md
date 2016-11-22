---
title: Hello World
categories: hexo
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## 开发版本

### 测试中文

**重要**: 在发布后构建的文件在 Github 仓库的 `/dist`  文件夹。为了使用 Github 上 Vue 最新的资源，你得自己构建。 

#### 这是H4

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

### 测一下css

``` css
a{
    font-size:14px;
}
```

### 测一下html

``` html
<div id="app-2">
  <span v-bind:title="message">
    Hover your mouse over me for a few seconds to see my dynamically bound title!
  </span>
</div>
```

### 测一下js

``` js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```

### 测一下li

- 这是*li1*
- 这是~~li2~~
- 这是**li3**

### 测一下引用

>朝辞白帝彩云间
>千里江陵一日还
>两岸猿声啼不住
>轻舟已过万重山

A common need for data binding is manipulating an element's class list and its inline styles. Since they are both attributes, we can use `v-bind` to handle them: we just need to calculate a final string with our expressions. However, meddling with string concatenation is annoying and error-prone. For this reason, Vue provides special enhancements when `v-bind` is used with `class` and `style`. In addition to strings, the expressions can also evaluate to objects or arrays.

## Binding HTML Classes

### Object Syntax

We can pass an object to `v-bind:class` to dynamically toggle classes:

``` html
<div v-bind:class="{ active: isActive }"></div>
```

The above syntax means the presence of the `active` class will be determined by the [truthiness](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) of the data property `isActive`.

You can have multiple classes toggled by having more fields in the object. In addition, the `v-bind:class` directive can also co-exist with the plain `class` attribute. So given the following template:

``` html
<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>
```

And the following data:

``` js
data: {
  isActive: true,
  hasError: false
}
```

It will render:

``` html
<div class="static active"></div>
```

When `isActive` or `hasError` changes, the class list will be updated accordingly. For example, if `hasError` becomes `true`, the class list will become `"static active text-danger"`.

The bound object doesn't have to be inline:

``` html
<div v-bind:class="classObject"></div>
```
``` js
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
```

This will render the same result. We can also bind to a [computed property](computed.html) that returns an object. This is a common and powerful pattern:

``` html
<div v-bind:class="classObject"></div>
```
``` js
data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal',
    }
  }
}
```

### Array Syntax

We can pass an array to `v-bind:class` to apply a list of classes:

``` html
<div v-bind:class="[activeClass, errorClass]">
```
``` js
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
```

Which will render:

``` html
<div class="active text-danger"></div>
```

If you would like to also toggle a class in the list conditionally, you can do it with a ternary expression:

``` html
<div v-bind:class="[isActive ? activeClass : '', errorClass]">
```

This will always apply `errorClass`, but will only apply `activeClass` when `isActive` is `true`.

However, this can be a bit verbose if you have multiple conditional classes. That's why it's also possible to use the object syntax inside array syntax:

``` html
<div v-bind:class="[{ active: isActive }, errorClass]">
```

### With Components

> This section assumes knowledge of [Vue Components](components.html). Feel free to skip it and come back later.

When you use the `class` attribute on a custom component, those classes will be added to the component's root element. Existing classes on this element will not be overwritten.

For example, if you declare this component:

``` js
Vue.component('my-component', {
  template: '<p class="foo bar">Hi</p>'
})
```

Then add some classes when using it:

``` html
<my-component class="baz boo"></my-component>
```

The rendered HTML will be:

``` html
<p class="foo bar baz boo">Hi</p>
```

The same is true for class bindings:

``` html
<my-component v-bind:class="{ active: isActive }"></my-component>
```

When `isActive` is truthy, the rendered HTML will be:

``` html
<p class="foo bar active"></p>
```

## Binding Inline Styles

### Object Syntax

The object syntax for `v-bind:style` is pretty straightforward - it looks almost like CSS, except it's a JavaScript object. You can use either camelCase or kebab-case for the CSS property names:

``` html
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```
``` js
data: {
  activeColor: 'red',
  fontSize: 30
}
```

It is often a good idea to bind to a style object directly so that the template is cleaner:

``` html
<div v-bind:style="styleObject"></div>
```
``` js
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```

Again, the object syntax is often used in conjunction with computed properties that return objects.

### Array Syntax

The array syntax for `v-bind:style` allows you to apply multiple style objects to the same element:

``` html
<div v-bind:style="[baseStyles, overridingStyles]">
```

### Auto-prefixing

When you use a CSS property that requires vendor prefixes in `v-bind:style`, for example `transform`, Vue will automatically detect and add appropriate prefixes to the applied styles.


### Compatibility Note

Vue does **not** support IE8 and below, because it uses ECMAScript 5 features that are un-shimmable in IE8. However it supports all [ECMAScript 5 compliant browsers](http://caniuse.com/#feat=es5).

### Release Notes

Detailed release notes for each version are available on [GitHub](https://github.com/vuejs/vue/releases).

## Standalone

Simply download and include with a script tag. `Vue` will be registered as a global variable.

<p class="tip">Don't use the minified version during development. You will miss out all the nice warnings for common mistakes!</p>

<div id="downloads">
<a class="button" href="/js/vue.js" download>Development Version</a><span class="light info">With full warnings and debug mode</span>

<a class="button" href="/js/vue.min.js" download>Production Version</a><span class="light info">Warnings stripped, {{gz_size}}kb min+gzip</span>
</div>

### CDN

Recommended: [unpkg](https://unpkg.com/vue/dist/vue.js), which will reflect the latest version as soon as it is published to npm. You can also browse the source of the npm package at [unpkg.com/vue/](https://unpkg.com/vue/).

Also available on [jsdelivr](//cdn.jsdelivr.net/vue/{{vue_version}}/vue.js) or [cdnjs](//cdnjs.cloudflare.com/ajax/libs/vue/{{vue_version}}/vue.js), but these two services take some time to sync so the latest release may not be available yet.

## NPM

NPM is the recommended installation method when building large scale applications with Vue. It pairs nicely with module bundlers such as [Webpack](http://webpack.github.io/) or [Browserify](http://browserify.org/). Vue also provides accompanying tools for authoring [Single File Components](single-file-components.html).

``` bash
# latest stable
$ npm install vue
```

### Standalone vs. Runtime-only Build

There are two builds available, the standalone build and the runtime-only build. The difference being that the former includes the **template compiler** and the latter does not.

The template compiler is responsible for compiling Vue template strings into pure JavaScript render functions. If you want to use the `template` option, then you need the compiler.

- The standalone build includes the compiler and supports the `template` option. **It also relies on the presence of browser APIs so you cannot use it for server-side rendering.**

- The runtime-only build does not include the template compiler, and does not support the `template` option. You can only use the `render` option when using the runtime-only build, but it works with single-file components, because single-file components' templates are pre-compiled into `render` functions during the build step. The runtime-only build is roughly 30% lighter-weight than the standalone build, weighing only {{ro_gz_size}}kb min+gzip.

By default, the NPM package exports the **runtime-only** build. To use the standalone build, add the following alias to your Webpack config:

``` js
resolve: {
  alias: {
    'vue$': 'vue/dist/vue.js'
  }
}
```


More info: [Deployment](https://hexo.io/docs/deployment.html)


