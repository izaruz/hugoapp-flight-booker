<template>
  <div class="container-fluid"> 
    <header>
      <h5>Isaac Villatoro | Flight booker</h5>
    </header>
    <Booker />
  </div>
</template>

<script>
import Booker from './components/Booker.vue'

export default {
  name: 'App',
  components: {
    Booker
  }
}
</script>

<style>
body {
  background: #f2f2fe;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #eefafe, #f2f2fe);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #eefafe, #f2f2fe); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #291c5f;
}
header{
  display: flex;
  padding: 2rem 4rem;
}
</style>
