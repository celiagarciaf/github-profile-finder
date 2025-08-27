<template>
  <h1>Bienvenido al buscador de GitHub</h1>
  <img src="./assets/logo.svg" alt="Logo Vue">
  <GitHub msg="Welcome to Your Vue.js App"/>
</template>

<script>
import GitHub from './components/GitHub.vue'

export default {
  name: 'App',
  components: {
    GitHub,
  }
}

</script>
