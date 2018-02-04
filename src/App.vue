<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color:#444;
  font-size: 14px;
  height:100%;
}
html,body{
  padding:0;
  margin:0;
}
.content{
  width:1200px;
  margin:0 auto;
  /* border:1px solid red; */
}
*{
  box-sizing: border-box;
}
p{
  padding:0;
  margin:0;
}
</style>
