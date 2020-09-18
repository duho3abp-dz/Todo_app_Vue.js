<template>
  <div>
    <ul>
        <TodoItem 
            v-for="todo of todos" 
            v-bind:todo="todo"
            @todo-remove="removeTodo"
        />
    </ul>
  </div>
</template>

<script>
import TodoItem from './TodoItem';
export default {
    props: ['todos'],
    components: {TodoItem},
    methods: {
        removeTodo(id) {
            this.$emit('todo-remove', id);
        }
    }
}
</script>

<style scoped>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>