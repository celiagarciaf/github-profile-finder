<template>
  <div class="repo-card">
    <p><strong>Nombre:</strong> {{ datosRep.name }}</p>
    <p><strong>URL:</strong> <a :href="datosRep.html_url" target="_blank">{{ datosRep.html_url }}</a></p>
    <p><strong>Descripción:</strong> {{ datosRep.description }}</p>
    <div class="forks">
      <strong>Forks:</strong> {{ datosRep.forks_count }}
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
p{
    color: black;
}
.repo-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 1rem;
  background: #f9f9f9;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}
.repo-card a {
  color: #42b983; 
  text-decoration: none;
}
.repo-card a:hover {
  text-decoration: underline;
}
.forks {
  text-align: right;
  font-size: 0.9rem;
  color: #555;
}
</style>
