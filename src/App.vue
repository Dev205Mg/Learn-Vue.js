<template>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input 
      type="text" 
      placeholder="Ajouter votre todo"
      v-model="newTodo">
      <button :disabled="newTodo.length <= 3">Ajouter</button>
    </fieldset>
  </form>
  <div v-if="todos.length === 0">
    Aucune tache a faire pour le moment :(
  </div>
  <div v-else>
    <ul>
    <li 
      v-for="todo in sortedTodos()"
      :key="todo.date"
      :class="{completed: todo.completed}"
      >
      <label>
        <input type="checkbox" v-model="todo.completed">
        {{ todo.title }}
      </label>
    </li>
  </ul>

  <label>
    <input type="checkbox" v-model="hideTodosCompleted">
    Masquer les taches completées
  </label>

  </div>

</template>

<script setup>
  import { ref } from 'vue';

  const newTodo = ref('')
  const hideTodosCompleted = ref(false)
  const todos = ref([])

  const addTodo = () => {
    todos.value.push({
      title: newTodo.value,
      completed: false,
      date: Date.now()
    })

    newTodo.value = ''
  }

  const sortedTodos = () =>{
    const sortedTodos = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
    if(hideTodosCompleted.value === true){
      return sortedTodos.filter(t => t.completed === false)
    }
    return sortedTodos
  }

</script>

<style>
  .completed{
    opacity: .5;
    text-decoration: line-through;
  }
</style>
