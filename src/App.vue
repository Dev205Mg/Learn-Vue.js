<template>
  <p>Compteur: {{ count }}</p>
  <button @click="increment">Incrémenter</button>
  <button @click="count--">Décrementer</button>
</template>

<script setup>
  import { ref } from 'vue';

  const count = ref(0)
  const increment = (event) => {
    count.value++
    console.log(event)
  }

</script>
