<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/dashboard">Dashboard</router-link> |
    <router-link to="/about">About Us</router-link>
  </div>
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
  padding-bottom: 150px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  z-index: 1;
}

#nav {
  margin-bottom: 10px;
  border-bottom: 3px solid #42b983;
  padding: 30px;
  background: #2c3e50;
}

#nav a {
  font-weight: bold;
  color: #fff;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
