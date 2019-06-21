<template>
  <div id="app">
    <b-container>
      <b-row>
        <b-col><div class="top">Shuffle Sentence</div></b-col>
        <b-col>
          <div id="nav">
          <router-link to="/">ホーム</router-link> |
          <router-link to="/about">使い方・便利リンク集</router-link>
        </div>
        </b-col>
      </b-row>
      <router-view/>
    </b-container>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default class App extends Vue {
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.top {
  padding: 30px;
  font-size: 120%;
  font-weight: 600;
}
</style>
