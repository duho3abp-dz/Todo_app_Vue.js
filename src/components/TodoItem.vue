<template>
    <li>
        <span v-bind:class="{done: todo.completed}">
            <input type="checkbox" v-if="todo.completed" checked @change="todo.completed = !todo.completed">
            <input type="checkbox" v-else @change="todo.completed = !todo.completed">
            <strong>{{ index + 1 }}</strong>
            {{ todo.title | upperCase }}
        </span>
        <button class="delete" @click="$emit('todo-remove', todo.id)">&times;</button>
    </li>
</template>

<script>
export default {
    props: {
        todo: {
        type: Object,
        required: true
        },
        index: {
            type: Number
        }
    },
    filters: {
        upperCase(value) {
            return value.toUpperCase();
        }
    }
}
</script>

<style scoped>
    li {
        border: 1px solid #ccc;
        display: flex;
        justify-content: space-between;
        padding: .5rem 2rem;
        margin-bottom: 1rem;
    }
    .delete {
        background: red;
        color: #fff;
        border-radius: 50%;
        font-weight: bold;
        outline: none;
    }
    input {
        margin-right: 1rem;
    }
    .done {
        text-decoration: line-through;
    }
</style>