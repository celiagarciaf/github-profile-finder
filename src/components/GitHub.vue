<template>
  <div class="github-container">
    <div class="search-box">
      <label for="name">🔍 Nombre de usuario:</label>
      <input
        type="text"
        id="name"
        v-model="user"
        @keydown.enter="obtenerUsuario"
        :disabled="deshabilitado"
        placeholder="Escribe un usuario de GitHub..."
      />
      <button @click="obtenerUsuario" :disabled="deshabilitado">
        Buscar
      </button>
    </div>

    <div v-if="inicio" class="user-card">
      <div v-if="userExist">
        <img :src="userData.avatar_url" alt="avatar" class="avatar" />
        <h2>{{ userData.login }}</h2>
        <a :href="userData.html_url" target="_blank">
          {{ userData.html_url }}
        </a>
        <button class="repos-btn" @click="obtenerRepositorios" :disabled="deshabilitado">
          Ver Repositorios
        </button>
      </div>

      <div v-else class="error-msg">
        <p>⚠️ El usuario no existe</p>
      </div>
    </div>

    <div class="repos">
      <GitHubRepo
        v-for="rep in listadoReps"
        :datosRep="rep"
        :key="rep.id"
      />
    </div>
  </div>
</template>

<script>
import GitHubRepo from './GitHubRepo.vue'
import axios from "axios"

export default {
  components: { GitHubRepo },
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
  methods: {
    async obtenerUsuario() {
      this.userExist = true
      this.inicio = true
      this.deshabilitado = true
      this.listadoReps = []

      const url = "https://api.github.com/users/" + this.user
      await axios.get(url)
        .then(response => {
          this.userData = response.data
        })
        .catch(() => {
          this.userExist = false
          this.userData = {}
        })
        .finally(() => {
          this.deshabilitado = false
        })
    },

    async obtenerRepositorios() {
      const urlRep = "https://api.github.com/users/" + this.user + "/repos"
      this.deshabilitado = true

      await axios.get(urlRep)
        .then(response => {
          this.listadoReps = response.data
        })
        .finally(() => {
          this.deshabilitado = false
        })
    }
  }
}
</script>

<style scoped>
.github-container {
  max-width: 800px;
  margin: 2rem auto;
  padding: 1.5rem;
  background: #f9f9f9;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  font-family: Arial, sans-serif;
}

.search-box {
  display: flex;
  gap: 0.5rem;
  align-items: center;
  margin-bottom: 1rem;
}

.search-box input {
  flex: 1;
  padding: 0.6rem;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.search-box button {
  padding: 0.6rem 1rem;
  background: #42b983;
  border: none;
  border-radius: 8px;
  color: white;
  cursor: pointer;
  transition: background 0.2s;
}

.search-box button:hover:not(:disabled) {
  background: #36996e;
}

.search-box button:disabled {
  background: #a5d6bd;
  cursor: not-allowed;
}

.user-card {
  text-align: center;
  margin: 1rem 0;
  padding: 1rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.08);
}

.user-card h2 {
  margin: 0.5rem 0;
  color: #333;
}

.user-card a {
  display: block;
  margin-bottom: 1rem;
  color: #35495e;
  text-decoration: none;
}

.user-card a:hover {
  text-decoration: underline;
}

.avatar {
  border-radius: 50%;
  width: 120px;
  margin-bottom: 0.5rem;
}

.repos-btn {
  padding: 0.5rem 1rem;
  border: none;
  background: #35495e;
  color: white;
  border-radius: 8px;
  cursor: pointer;
}

.repos-btn:hover:not(:disabled) {
  background: #2a3746;
}

.repos-btn:disabled {
  background: #999;
  cursor: not-allowed;
}

.error-msg {
  padding: 1rem;
  background: #ffefef;
  color: #c0392b;
  border-radius: 8px;
  font-weight: bold;
}

.repos {
  margin-top: 1.5rem;
}
</style>
