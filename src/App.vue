<template>
  <div id="app">
    <Ghibli/>
  </div>
</template>

<script>
import Ghibli from "@/components/Ghibli.vue"

export default {
  name: 'App',
  components: {
    Ghibli
  },
  methods:{
  }
}
</script>

<style>
body{
  height: 100%;
  width: 100%;
  background: url(@/assets/ghib.jpeg) center repeat fixed;
  background-size: 20%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
