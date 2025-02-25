<template>
  <p>Compteur: {{ count }}</p>
  <div v-show="count>=5">Bravo ! Vous avez cliquer 5 fois</div>
  <div v-if="count <= 4">Non ! Pas encore cliquer 5 fois</div>
  <button @click="increment">Incrémenter</button>
  <button @click="count--">Décrementer</button>
  <hr>
  <button @click="sortMovie">Réorganiser</button>
  <form action="" @submit.prevent="addMovie">
    <input 
      type="text" 
      placeholder="Nouveau Film"
      v-model="movieName">
      <button >Ajouter</button>
  </form>
  <ul>
    <li 
      v-for="movie in movies"
      :key="movie"
      >
      {{ movie }} <button @click="deleteMovie(movie)">Supprimer</button>
    </li>
  </ul>
</template>

<script setup>
  import { ref } from 'vue';

  const count = ref(0)
  const movieName = ref('')
  const movies = ref([
    'Matrix',
    'Titanic',
    'Moana',
    'Merlin',
    'Tomb Rider'
  ])
  const increment = (event) => {
    count.value++
  }

  const deleteMovie = (movie) => {
    console.log(movie)
    movies.value = movies.value.filter( m => m !== movie)
    console.log(movies)
  }

  const sortMovie = () => {
    movies.value.sort()
  }

  const addMovie = () => {
    movies.value.push(movieName.value)
    movieName.value = ''
  }

</script>
