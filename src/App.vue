<template>
  <router-view/>
  <Footer/>
</template>

<script>
import Footer from '@/components/Footer.vue'

export default {
  components: {
    Footer
  }
}
</script>

<style>
#app {
  text-align: center;
  padding-bottom: 150px;
}

/* #nav a.router-link-exact-active {
  color: #42b983;
} */
</style>
