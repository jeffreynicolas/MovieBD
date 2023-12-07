<script setup>
import { ref, onMounted } from 'vue'
import Loading from 'vue-loading-overlay'
import api from '@/plugins/axios'
import genreStore from '@/stores/genre'

const genres = ref([])
const isLoading = ref(false)
const getGenreName = (id) => genres.value.find((genre) => genre.id === id).name
onMounted(async () => {
  isLoading.value = true
  await genreStore.getAllGenres('movie')
  isLoading.value = false
})

const formatDate = (date) => new Date(date).toLocaleDateString('pt-BR')

const movies = ref([])

const listMovies = async (genreId) => {
  isLoading.value = true
  const response = await api.get('discover/movie', {
    params: {
      with_genres: genreId,
      language: 'pt-BR'
    }
  })
  movies.value = response.data.results
  isLoading.value = false
}
</script>
<template>
  <div class="home">
    <h1>Bem-vindo ao Nosso Cine</h1>
    <div class="movie-list">
      <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" :alt="movie.title" />
      <img src="filme2.jpg" alt="Filme 2" />
      <img src="filme3.jpg" alt="Filme 3" />
    </div>
  </div>
</template>

<style scoped>
.home {
  text-align: center;
  padding: 20px;
}

h1 {
  color: #333;
  font-size: 2rem;
  margin-bottom: 20px;
}

.movie-list {
  display: flex;
  justify-content: center;
  gap: 20px;
}

.movie-list img {
  max-width: 200px;
  height: auto;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease-in-out;
}

.movie-list img:hover {
  transform: scale(1.1);
}
</style>
