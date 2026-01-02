<template>
  <div id="app">
    <NavbarTop v-if="$route.name !== 'start'" />
    <router-view />
  </div>
</template>

<script>
import NavbarTop from '@/components/Navbar.vue'

export default {
  name: 'App',
  components: {
    NavbarTop
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body, #app {
  width: 100%;
  height: 100%;
  background: #1c1B20;
  color: white;
  font-family: 'DM Sans', sans-serif;
}
</style>