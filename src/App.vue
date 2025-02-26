<template>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input 
        type="text" 
        placeholder="Ajouter un todo"
        v-model="newTodo"
        >
      <button :disabled="newTodo.length <= 3">Ajouter</button>
    </fieldset>
  </form>

  <div v-if="todos.length === 0">
    Vous n'avez pas encore de tache :(
  </div>
  <div v-else>
    <ul>
      <li 
        v-for="todo in todoSorted()"
        :key="todo.date"
        :class="{completed: todo.completed}"
        >
        <label>
          <input 
            type="checkbox" 
            v-model="todo.completed"
            :checked="todo.completed"
            >
          {{ todo.title }}
        </label>
      </li>

    </ul>
    <div>
      <label>
        <input 
          type="checkbox"
          v-model="hideTodos">
        Masquer les taches qui sont deja fait 
      </label>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

  const newTodo = ref('')
  const hideTodos = ref(false)
  const todos = ref([])

  const addTodo = () => {
    todos.value.push({
      title: newTodo.value,
      completed: false,
      date: Date.now()
    })

    newTodo.value = ''
  }

  const todoSorted = () => {
    const todoSorted = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
    if(hideTodos.value === true){
      return todoSorted.filter(t => t.completed !== true)
    }
    return todoSorted
  }
  
</script>

<style>
  .completed {
    opacity: .5;
    text-decoration: line-through;
  }
</style>