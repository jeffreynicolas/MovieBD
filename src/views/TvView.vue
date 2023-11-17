<script setup>
import { ref, onMounted } from 'vue'
import api from '@/plugins/axios'
import genreStore from '@/stores/genre'

// const genres = ref([])
const isLoading = ref(false)

onMounted(async () => {
  isLoading.value = true
  await genreStore.getAllGenres('tv')
  isLoading.value = false
})



const tv = ref([]);

const listtv = async (genreId) => {
    const response = await api.get('discover/tv', {
        params: {
            with_genres: genreId,
            language: 'pt-BR'
        }
    });
    tv.value = response.data.results
};    

</script>

<template>
  <h1>Programas de TV</h1>
  <ul class="genre-list">
    <li
      v-for="genre in genreStore.genres"
      :key="genre.id"
      @click="listtv(genre.id)"
      class="genre-item"
    >
    
      {{ genre.name }}
    
    </li>
  </ul>


  <div class="tv-list">
  <div v-for="tv in tv" :key="tv.id" class="tv-card">
    
    <img :src="`https://image.tmdb.org/t/p/w500${tv.poster_path}`" :alt="tv.title" />
    <div class="tv-details">
      <p class="tv-title">{{ tv.title }}</p>
      <p class="tv-release-date">{{ tv.release_date }}</p>
      <span v-for="genre_id in tv.genre_ids" :key="genre_id" @click="listtv(genre_id)">
    {{ genreStore.getGenreName(genre_id) }}
  </span>
    </div>
    
  </div>
</div>


</template>

<style scoped>
.genre-list {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 2rem;
  list-style: none;
  padding: 0;
}

.genre-item {
  background-color: #5d6424;
  border-radius: 1rem;
  padding: 0.5rem 1rem;
  align-self: center;
  color: #fff;
  display: flex;
  justify-content: center;
}

.genre-item:hover {
  cursor: pointer;
  background-color: #7d8a2e;
  box-shadow: 0 0 0.5rem #5d6424;
}
.tv-list {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.tv-card {
  width: 15rem;
  height: 30rem;
  border-radius: 0.5rem;
  overflow: hidden;
  box-shadow: 0 0 0.5rem #000;
}

.tv-card img {
  width: 100%;
  height: 20rem;
  border-radius: 0.5rem;
  box-shadow: 0 0 0.5rem #000;
}

.tv-details {
  padding: 0 0.5rem;
}

.tv-title {
  font-size: 1.1rem;
  font-weight: bold;
  line-height: 1.3rem;
  height: 3.2rem;
}
</style>
