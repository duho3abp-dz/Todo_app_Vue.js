<template>
  <div>
    <Error v-if="error"/>
    <Loader v-else-if="loading"/>
    <TodoList 
        v-bind:todos="todos"
        v-else-if="todos.length"
        @todo-remove="removeTodo"
    />
    <p v-else>No Todos!</p>
    
    <hr>
    <AddTodo 
      @add-todo="onSubmit"
    />
    <hr>
    <router-link to="/">Home</router-link>
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