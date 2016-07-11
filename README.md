# vue-yummy-notie

> a clean and simple notification component for vue.js. Deeply inspired by Notie.js.
> [Demo](http://lab.myriptide.com/vue-notie/)

![preview](/yummy-notie-m.gif?raw=true "Demo")

## How to use

Components are one of the most powerful features of Vue.js. Yummy notie is a component which can help you to alert users.
Since it is a component instead of a plugin, all you need to do is import the module and pass options with props or vuex.

## Installation

The sample was set up by vue-cli's webpack template. You need to import Notification.vue in the component folder into your project. Then you can regist it and use it in the HTML template.

```HTML
<template>
  <notification
  :options.sync="options"
  :show.sync="showNotification"></notification>
</template>

<script>
import Notification from './components/Notification'

export default {
  components: { Notification },
  data () {
    return {
      showNotification: false,
      options: {}
    }
  }
}
</script>
```

## Make a notice

We need to pass two data into Notification.vue with props or vuex. Data 'show' controls the display of the notice. You need to set ```show = true```to init a notice, and also pass the content you want to show by setting 'options'.

## options

```javascript
options: {
  autoClose: true,
  backgroundColor: '#769FCD',
  barColor: '#415f77',
  countdownBar: true,
  content: 'The content of the notification.',
  showTime: 5000,
  textColor: '#fff'
}
```