<template>
  <div id="app">
    <h1>Todo application</h1>
    <hr>
    <TodoList 
      v-bind:todos="todos"
      @todo-remove="removeTodo"
    />
    <AddTodo 
      @add-todo="onSubmit"
    />
  </div>
</template>

<script>
import TodoList from './components/TodoList';
import AddTodo from './components/AddTodo';
export default {
  name: 'App',
  components: {TodoList, AddTodo},
  data() {
    return {
      todos: [
        {id: 1, title: 'Buy oil', completed: false},
        {id: 2, title: 'Buy bread', completed: false},
        {id: 3, title: 'Buy beer', completed: false}
      ]
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
