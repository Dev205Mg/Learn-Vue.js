<template>
  <p>Compteur: {{ count }}</p>
  <div v-show="count>=5">Bravo ! Vous avez cliquer 5 fois</div>
  <div v-if="count <= 4">Non ! Pas encore cliquer 5 fois</div>
  <button @click="increment">Incrémenter</button>
  <button @click="count--">Décrementer</button>
</template>

<script setup>
  import { ref } from 'vue';

  const count = ref(0)
  const increment = (event) => {
    count.value++
  }

</script>
