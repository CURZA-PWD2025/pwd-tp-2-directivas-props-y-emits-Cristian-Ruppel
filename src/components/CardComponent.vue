<template>
    <div class="card">
      <img v-if="pelicula.portada" :src="pelicula.portada" alt="Portada">
      <p v-show="!pelicula.portada">🎬 Portada no disponible</p>
      <div class="card-content">
        <h2>{{ pelicula.titulo }}</h2>
        <p><strong>Director:</strong> {{ pelicula.director }}</p>
        <p><strong>Año:</strong> {{ pelicula.anio }}</p>
        <button @click="toggleLike" :class="{ liked: pelicula.likes > 0 }">
          ❤️ {{ pelicula.likes }}
        </button>
      </div>
    </div>
  </template>
  
  <script setup>
  const props = defineProps({
    pelicula: {
      type: Object,
      required: true
    }
  })
  
  const emit = defineEmits(['update_likes'])
  
  const toggleLike = () => {
    emit('update_likes', props.pelicula.id)
  }
  </script>
  
  <style scoped>
  .card {
    border: 1px solid #ddd;
    border-radius: 8px;
    overflow: hidden;
    background: white;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  }
  .card img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }
  .card-content {
    padding: 1rem;
  }
  button {
    background: none;
    border: 1px solid #ccc;
    padding: 0.5rem 1rem;
    cursor: pointer;
    transition: all 0.3s;
  }
  button.liked {
    background: #ff6b6b;
    border-color: #ff6b6b;
    color: white;
  }
  </style>