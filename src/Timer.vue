<template>
  <div>
    Temps : {{ time }}
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

const time = ref(0)
let timer

onMounted(() => {
  timer = setInterval(() => {
    console.log('Increment')
    time.value++
  }, 1000)
})

onUnmounted(() => {
  clearInterval(timer)
})

</script>