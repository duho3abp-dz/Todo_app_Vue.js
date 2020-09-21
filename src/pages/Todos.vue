<template>
  <div>
    <h2>Todo List</h2>
    <router-link to="/">Home</router-link>

    <hr>
    <AddTodo @add-todo="onSubmit" />
    <hr>

    <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not-completed</option>
    </select>
    

    <Error v-if="error"/>
    <Loader v-else-if="loading" />
    <TodoList 
        v-bind:todos="filteredTodos"
        v-else-if="filteredTodos.length"
        @todo-remove="removeTodo"
    />
    <p v-else>No Todos!</p>

  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';
import Loader from '@/components/Loader';
import Error from '@/components/Error';

export default {
  name: 'App',
  components: {TodoList, AddTodo, Loader, Error},
  data() {
    return {
      error: false,
      filter: 'all',
      loading: true,
      todos: []
    }
  },
  mounted() {
      fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => this.todos = json)
        .catch(err => this.error = true)
        .finally(res => this.loading = false);
  },
  computed: {
      filteredTodos() {
          if (this.filter === 'all') {
              return this.todos;
          } 
          if (this.filter === 'completed') {
              return this.todos.filter(obj => obj.completed);
          } 
          if (this.filter === 'not-completed') {
              return this.todos.filter(obj => !obj.completed);
          } 
      }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(obj => obj.id !== id);
    },
    onSubmit(value) {
      const newObj = {
        id: new Date(), 
        title: value, 
        completed: false
      };
      this.todos.push(newObj);
    }
  }
}
</script>

<style scoped>
    select {
        margin-bottom: 10px;
    }
</style>