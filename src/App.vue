<template>
  <div class="app">
    <h1>Mis Películas</h1>
    <div class="cards-container">
      <CardComponent 
        v-for="pelicula in peliculasList" 
        :key="pelicula.id" 
        :pelicula="pelicula"
        @update_likes="handleLike"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CardComponent from './components/CardComponent.vue'
import peliculas from './movies.ts'

const peliculasList = ref([...peliculas])

const handleLike = (id) => {
  peliculasList.value = peliculasList.value.map(p => 
    p.id === id ? { ...p, likes: p.likes === 0 ? 1 : 0 } : p
  )
}
</script>

<style scoped>
.app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}
.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1rem;
}
</style>