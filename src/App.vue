<template>
<body>
  <div class="grid-container">
      <div><HomePage/></div>
      <div><SearchBar/></div>
      <div></div>
  </div>
  </body>
</template>

<script>
import HomePage from './components/HomePage.vue'
import SearchBar from './components/SearchBar.vue'

export default {
  name: 'App',
  components: {
    HomePage,
    SearchBar,
  }
}
</script>

<style>
html{
  background-color:rgb(83, 131, 232) !important
}

</style>
