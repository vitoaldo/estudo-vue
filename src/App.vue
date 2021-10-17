<template>
  <p v-for="todo in doneTodos" :key="todo.text">{{ todo.text }}</p>
  <button @click="checkAllTodos">Finalizar</button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

interface Todo {
  text: string
  done: boolean
}

export default defineComponent({
  data() {
    return {
      todos: [] as Todo[],
    }
  },
  created() {
    this.todos = [
      { text: 'Estudar Typescript', done: true },
      { text: 'Lavar os pratos', done: false },
      { text: 'Aprender Nuxt.js', done: true },
    ]
  },
  computed: {
    doneTodos(): Todo[] {
      return this.todos.filter((todo) => todo.done)
    },
  },
  methods: {
    checkAllTodos(): void {
      this.todos = this.todos.map(({ text }) => {
        return { text, done: true }
      })
    },
  },
  watch: {
    todos(newValue: Todo[]) {
      const isFinished = !newValue.some(({ done }) => !done)

      if (isFinished) {
        alert('Tarefas concluidas!')
      }
    },
  },
})
</script>
