<template>
  <div>
    <p>Nombre: {{ datosRep.name }}</p>
    <p>URL: {{ datosRep.html_url }}</p>
    <tittle>Descripción: {{ datosRep.description }}</tittle>
    <div class="forks">
      Número forks:
      {{ datosRep.forks_count }}
    </div>
  </div>
</template>

<script>

export default {
  name: 'GitHubRepo',
  props: [
    "datosRep"
  ]
}
</script>

<style scoped>
.forks{
  text-align: right;
}
</style>
