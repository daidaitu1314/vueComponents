<template>
  <div id="app">
    <img @click="showPreviewImage" src="./assets/logo.png">
    <img src="./assets/nav01.png" alt="">
    <img src="./assets/nav03.png" alt="">
    <img src="./assets/p01.jpg" alt="">
    <img src="./assets/p02.jpg" alt="">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
    <PreviewImage :list="imgList" :showPreviewImage="false" ref="PreviewImage"></PreviewImage>
  </div>
</template>

<script>
import PreviewImage from './components/PreviewImage.vue'
export default {
  name: 'app',
  components:{PreviewImage},
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      imgList:[
        './dist/nav01.png',
        './dist/nav03.png',
        './dist/p01.jpg',
        './dist/p02.jpg'
      ]
    }
  },
  methods:{
    showPreviewImage(){
      this.$refs.PreviewImage.showPreview();
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
