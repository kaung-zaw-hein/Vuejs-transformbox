<template>
    <Box></Box>
</template>

<script>
import Box from './components/Box'
export default {
  name: 'App',
  components: {
    Box,
  }
}
</script>

<style>
body{
  background:chocolate;
  overflow:hidden;
  display:flex;
  align-items:center;
  justify-content:center;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  margin-top: 100px;
}
main{
  display: flex;
  width:1000px;
}
</style>
