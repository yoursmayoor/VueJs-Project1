<template>
<Navbar />
  <router-view/>
</template>
<script>
import Navbar from './views/Navbar.vue'
  
export default{
components: {Navbar}
}
</script>


<style>
body{
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #555;
  margin: 50px auto;
  width: 600px;
}


</style>
