<template>
  <div>
    <div>
      Nombre de usuario: <input type="text" id="name" v-model="user" @keydown.enter="obtenerUsuario" :disabled="deshabilitado" >
    </div>

  <div v-if="inicio">
    <div v-if="userExist">
      {{ userData.login }}
      {{ userData.html_url }}
      <img :src="userData.avatar_url">
      <button @click="obtenerRepositorios">Repositorios</button>
    </div>
    
    <div v-else>
      <p>El usuario no existe</p>
    </div>
  </div>
    
  <div>
    <GitHubRepo v-for="rep in listadoReps" :datosRep="rep" :key="rep.id" />
  </div>

  </div>
</template>

<script>
import GitHubRepo from './GitHubRepo.vue'
import axios from "axios";

export default {
  components: {
    GitHubRepo
  },
  name: 'GitHub',
  data () {
  return {
    user: '',
    userData: {},
    inicio: false,
    userExist: true,
    listadoReps: [],
    deshabilitado: false
    }
  },
  props: {
  },
  methods: {
  obtenerUsuario: async function() {
    this.userExist = true;
    this.inicio = true;
    this.deshabilitado = true;
    this.listadoReps = [];

      var url = "https://api.github.com/users/" + this.user
      await axios.get(url).then(response => {
        this.userData = response.data;
        this.carga = true;
        document.getElementById("name").disabled = false;
      })
      .catch(error => {
        console.log(error)
        this.userExist = false; 
        this.userData = {};
      })
      .finally(() => {
        this.deshabilitado = false; 
      })
      },

    obtenerRepositorios: async function(){
      var urlRep = "https://api.github.com/users/" + this.user + "/repos";
      this.deshabilitado = true;

      await axios.get(urlRep).then(response =>{
        this.listadoReps = response.data
      })     
      .finally(() => {
        this.deshabilitado = false; 
      })
    }
    }
  }


</script>

<style scoped>

</style>
