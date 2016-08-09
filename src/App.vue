<template>
  <div id="app">
    <img class="logo" src="./assets/logo.png">
    <h1 v-text="mtitle">333333</h1>
    <h2>444555</h2>
    <p>
      Welcome to your Vue.js app!
    </p>
    <input type="text" v-model="newItem" placeholder="edit me" v-on:keyup.enter="msubmit">
    <ul>
      <li v-for="item in items" v-bind:class="[liclass , 'liclass' ,{'finish': item.isFinished} ]" v-on:click="doThis(item)">
        {{ item.label }}
      </li>
    </ul>

    <p>
      To get a better understanding of how this boilerplate works, check out
      <a href="http://vuejs-templates.github.io/webpack" target="_blank">its documentation</a>.
      It is also recommended to go through the docs for
      <a href="http://webpack.github.io/" target="_blank">Webpack</a> and
      <a href="http://vuejs.github.io/vue-loader/" target="_blank">vue-loader</a>.
      If you have any issues with the setup, please file an issue at this boilerplate's
      <a href="https://github.com/vuejs-templates/webpack" target="_blank">repository</a>.
    </p>
    <p>
      You may also want to checkout
      <a href="https://github.com/vuejs/vue-router/" target="_blank">vue-router</a> for routing and
      <a href="https://github.com/vuejs/vuex/" target="_blank">vuex</a> for state management.
    </p>
  </div>
</template>

<script>
import Store from './store.js'
console.log(Store)
export default {
  data: function () {
    return {
      mtitle: 'liuxc',
      qtitle: 'liuxc',
      items: Store.fetch(),
      liclass: 'liclass',
      finish: 'finish'
    }
  },
  watch: {
    items: {
      handler: function (val, oldval) {
        console.log(val, oldval)
        Store.save(val)
      },
      deep: true
    }
  },
  methods: {
    doThis: function (item) {
      console.log(item)
      item.isFinished = !item.isFinished
    },
    msubmit: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem = ''
    }
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  max-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
.finish{
  text-decoration: line-through;
}
.liclass{
  color: red;
}
</style>
