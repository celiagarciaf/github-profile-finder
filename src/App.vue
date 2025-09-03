<template>
  <div class="app-container">
    <header class="header">
      <img src="./assets/logo.svg" alt="Logo Vue" class="logo" />
      <h1>Buscador de GitHub en línea</h1>
    </header>

    <main>
      <GitHub msg="Welcome to Your Vue.js App" />
    </main>
  </div>
</template>

<script>
import GitHub from './components/GitHub.vue'

export default {
  name: 'App',
  components: { GitHub }
}
</script>

<style scoped>
.app-container {
  max-width: 900px;
  margin: 0 auto;
  padding: 35px;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  text-align: center;
  color: black;
  }

.header {
  margin-bottom: 2rem;
}

.logo {
  width: 100px;
  margin-bottom: 1rem;
}

h1 {
  font-size: 35px;
  color: #42b983;
}

main {
  background: #fff;
  padding: 1.5rem;
  border-radius: 13px;
}
</style>