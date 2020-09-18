<template>
  <div id="app">
    <h1>Todo application</h1><hr>
    <TodoList 
      v-bind:todos="todos"
      @todo-remove="removeTodo"
    />
  </div>
</template>

<script>
import TodoList from './components/TodoList';
export default {
  name: 'App',
  data() {
    return {
      todos: [
        {id: 1, title: 'Buy oil', completed: false},
        {id: 2, title: 'Buy bread', completed: false},
        {id: 3, title: 'Buy beer', completed: false}
      ]
    }
  },
  components: {TodoList},
  methods: {
    removeTodo(id) {
      let x = 1;
      this.todos = this.todos.filter(obj => obj.id !== id);
      this.todos = this.todos.map(obj => {
        obj.id = x;
        x++;
        return obj;
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
