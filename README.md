# vue-instagram

[![npm](https://img.shields.io/npm/v/vue-instagram.svg)](https://www.npmjs.com/package/vue-instagram)
[![npm](https://img.shields.io/npm/dt/vue-instagram.svg)](https://www.npmjs.com/package/vue-instagram)
[![npm](https://img.shields.io/npm/dm/vue-instagram.svg)](https://www.npmjs.com/package/vue-instagram)
[![npm](https://img.shields.io/npm/l/vue-instagram.svg)](http://opensource.org/licenses/MIT)

Instagram's feed fetcher component based on [Vue](https://vuejs.org/).

Fetch instagram feed via [`GET /me/media`](https://graph.instagram.com/me/media/)

**Works with Vue 2.***

## Changes

Now works with the new Instagram 2020 API. 
Based on this https://gitlab.com/snippets/1957175

## Demo

[My Instagram's feed](https://kevinongko.github.io/vue-instagram/)

## Installation

### Install via CDN
```html
<script src="https://unpkg.com/vue"></script>
<script src="https://unpkg.com/vue-instagram@3.1.0"></script>

<script>
  Vue.use(VueInstagram.default)
</script>
```

### Install via NPM
```sh
$ npm install https://github.com/nassosyian/vue-instagram --save
```

### Install via Yarn
```sh
$ yarn add https://github.com/nassosyian/vue-instagram
```

#### Register as Component
```js
import Vue from 'vue'
import VueInstagram from 'vue-instagram'

export default {
  name: 'App',

  components: {
    VueInstagram
  }
}
```

#### Register as Plugin
```js
import Vue from 'vue'
import VueInstagram from 'vue-instagram'

Vue.use(VueInstagram)
```

## Usage

Style your feeds using [scoped slot](https://vuejs.org/v2/guide/components.html#Scoped-Slots)

```vue
<template>
  <vue-instagram token="accessTokenHere" :count="5" fields="media_url,media_type,permalink,caption"  :mediatypes="['IMAGE', 'VIDEO', 'CAROUSEL_ALBUM']">
    <template v-slot:loading="props">
      <h1 v-if="props.loading" class="fancy-loading">Loading, please wait...</h1>
    </template>
    <template v-slot:feeds="props">
      <li class="fancy-list"> {{ props.feed.link }} </li>
    </template>
    <template v-slot:error="props">
      <div class="fancy-alert"> {{ props.error.error_message }} </div>
    </template>
  </vue-instagram>
</template>

<script>
import VueInstagram from 'vue-instagram'

export default {
  name: 'App',

  components: {
    VueInstagram
  }
}
</script>

```

## Props
|Props|Description|Type|Required|
|-----|-----------|----|--------|
|token|Instagram's access token|String|true|
|count|Numbers of feed to fetch|Number|true
|fields|The fields you want to access|String or Array|true
|mediatypes|Filter profile's feed by media type: image or video|String|false

## License

Vue-Instagram is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)

## Support

This is a fork of https://github.com/kevinongko/vue-instagram

Hello, I'm Kevin the maintainer of this project in my free time (which is getting lessen these days), if this project does help you in any way please consider to support me. Thanks :smiley:
- [One-time donation via Paypal](https://www.paypal.me/kevinongko)
