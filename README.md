# vue-marquee-text-component



`npm install vue-marquee-text-component` or `yarn add vue-marquee-text-component`

## Usage

The most common use case is to register the component globally.

```js
// in your main.js or similar file
import Vue from 'vue'
import MarqueeText from 'vue-marquee-text-component'

Vue.component('marquee-text', MarqueeText)
```

Alternatively you can do this to register the components:

```js
// HelloWorld.vue
import MarqueeText from 'vue-marquee-text-component'

export default {
  name: 'HelloWorld',
  components: {
    MarqueeText
  }
}
```

On your page you can now use html like this:

```html
<!-- simple marquee text -->
<marquee-text>
  Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna.
</marquee-text>

<!-- short text need more duplicates -->
<marquee-text :repeat="10">
  Short text =(
</marquee-text>

<!-- slow duration -->
<marquee-text :duration="30">
  Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna.
</marquee-text>
```

## Props

|Prop|Type|Default|Description
|-|-|-|-|
|duration|Number|15|Animation Duration
|repeat|Number|2|Number of repeat the Slot (It's important for to short content)
|paused|Boolean|false|The property specifies whether the animation is running or paused
|reverse|Boolean|false|Set animation-direction to reverse
|vertical|Booolean|false| set animation vertical

## Important information for dynamic content
If you change the content you need reload the component. For this use property `:key` [see more](https://vuejs.org/v2/api/#key)
```html
<!-- parse a unique key for reload the component  -->
<marquee-text :key="currentTrack.id">
  {{ currentTrack.title }}
</marquee-text>
```

## Build Setup

``` bash
yarn install
yarn run serve
yarn run build
yarn run lint
```
