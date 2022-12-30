<template>
  <NavBar />




  <RouterView />
</template>


<script>
import NavBar from './components/NavBar.vue';
export default {
  components: { NavBar },


}

</script>



<style>
body {
  background: #F0F2F5;
}
</style>
