<template>
  <Layout>
    <template #aside>
      Sidebar
    </template>
    <template #main>
      Main
    </template>
    <template #footer>
      Footer
    </template>
  </Layout>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input type="text" placeholder="Ajouter votre todo" v-model="newTodo">
      <button :disabled="newTodo.length <= 3">Ajouter</button>
    </fieldset>
  </form>
  <div v-if="todos.length === 0">
    Aucune tache a faire pour le moment :(
  </div>
  <div v-else>
    <ul>
      <li v-for="todo in sortedTodos" :key="todo.date" :class="{ completed: todo.completed }">
        <Checkbox 
          :label="todo.title"
          v-model="todo.completed"
          @check=" (p) => console.log('cocher', p)"
          @uncheck="console.log('decocher')"/>
      </li>
    </ul>

    <label>
      <input type="checkbox" v-model="hideTodosCompleted">
      Masquer les taches completées
    </label>

  </div>

  <p v-if="remainingTodo > 0">
    {{ remainingTodo }} tache{{ remainingTodo > 1 ? 's' : '' }} a faire
  </p>

  <Checkbox label="Bonjour"/>

</template>

<script setup>
import { computed, onMounted, ref } from 'vue';
import Checkbox from './Checkbox.vue';
import Button from './Button.vue';
import Layout from './Layout.vue';

const newTodo = ref('')
const hideTodosCompleted = ref(false)
const todos = ref([])

onMounted(() => {
  fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(r => r.json())
    .then(v => todos.value = v.map(todo => ({...todo, date: todo.id})))
})

const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now()
  })

  newTodo.value = ''
}

const sortedTodos = computed(() => {
  console.log('demo')
  const sortedTodos = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
  if (hideTodosCompleted.value === true) {
    return sortedTodos.filter(t => t.completed === false)
  }
  return sortedTodos
})

const remainingTodo = computed(() => {
  return todos.value.filter(t => t.completed === false).length
})

</script>

<style>
.completed {
  opacity: .5;
  text-decoration: line-through;
}
</style>
