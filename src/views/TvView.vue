<script setup>
import { ref, onMounted } from 'vue'
import api from '@/plugins/axios'
import genreStore from '@/stores/genre'

const isLoading = ref(false)

onMounted(async () => {
  isLoading.value = true
  await genreStore.getAllGenres('tv')
  isLoading.value = false
})

const tv = ref([])

const listtv = async (genreId) => {
  const response = await api.get('discover/tv', {
    params: {
      with_genres: genreId,
      language: 'pt-BR'
    }
  })
  tv.value = response.data.results
}
</script>

<template>
  <div class="tv-container">
    <h1 class="hero-title">Programas de Tv</h1>
    <ul class="genre-list">
      <li v-for="genre in genreStore.genres" :key="genre.id" @click="listtv(genre.id)" class="genre-item">
        {{ genre.name }}
      </li>
    </ul>

    <div class="tv-list">
      <div v-for="show in tv" :key="show.id" class="tv-card">
        <img :src="`https://image.tmdb.org/t/p/w500${show.poster_path}`" :alt="show.title" />
        <div class="tv-details">
          <p class="tv-title">{{ show.title }}</p>
          <p class="tv-release-date">{{ show.release_date }}</p>
          <div class="tv-genres">
            <span v-for="genre_id in show.genre_ids" :key="genre_id" @click="listtv(genre_id)" class="genre-tag">
              {{ genreStore.getGenreName(genre_id) }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
  
</template>

<style scoped>
.tv-container {
  text-align: center;
  padding: 20px;
  background-color: #101010;
  color: #fff;
  
}
.hero-title {
  font-size: 3rem;
  font-weight: bold;
  margin-bottom: 20px;
}

.genre-list {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 1rem;
  list-style: none;
  margin-bottom: 2rem;
}

.genre-item {
  background-color: #387250;
  border-radius: 1rem;
  padding: 0.5rem 1rem;
  color: #fff;
  transition: background-color 0.3s ease;
  cursor: pointer;
}

.genre-item:hover {
  background-color: #4e9e5f;
  box-shadow: 0 0 0.5rem #387250;
}


.tv-list {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
}

.tv-card {
  width: 15rem;
  height: 30rem;
  border-radius: 1rem;
  overflow: hidden;
  box-shadow: 0 0 1rem rgba(0, 0, 0, 0.3);
  transition: transform 0.3s ease-in-out;
  background-color: #202020;
}

.tv-card:hover {
  transform: scale(1.05);
}

.tv-card img {
  width: 100%;
  height: 20rem;
  border-top-left-radius: 1rem;
  border-top-right-radius: 1rem;
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.3);
}

.tv-details {
  padding: 1rem;
}

.tv-title {
  font-size: 0.9rem;
  font-weight: bold;
  line-height: 1.5;
  height: 3.5rem;
  margin-bottom: 0.5rem;
}


.tv-release-date {

  font-size: 1rem;
 
}

.tv-release-date:hover {
  color: var(--primary-color);
}


.tv-genres {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 1rem;
  justify-content: center;
}

.genre-tag {
  background-color: #086387;
  border-radius: 0.5rem;
  padding: 0.2rem 0.5rem;
  color: #fff;
  font-size: 0.8rem;
  font-weight: bold;
  transition: background-color 0.3s ease;
  cursor: pointer;
}

.genre-tag:hover {
  background-color: #455a08;
  box-shadow: 0 0 0.5rem #748708;
}
</style>
