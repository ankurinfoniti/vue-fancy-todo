<template>
    <div>
        <p>Completed Task: {{ todos.reduce((accumulator, current) => {return accumulator + current.done}, 0) }}</p>
        <p>Pending Task: {{ todos.reduce((accumulator, current) => {return accumulator + !current.done}, 0) }}</p>

        <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo(todo)" v-for="(todo, index) in todos" v-bind:key="index" v-bind:todo="todo"></todo>    
    </div>
</template>

<script>
import Todo from './Todo.vue'

export default {
    components: {
        Todo
    },
    props: ['todos'],
    methods: {
        deleteTodo(todo) {
            let todoIndex = this.todos.indexOf(todo);
            this.todos.splice(todoIndex, 1);
        },
        completeTodo(todo) {
            let todoIndex = this.todos.indexOf(todo);
            this.todos[todoIndex].done = true;
            this.$swal('Success!', 'To-Do completed!', 'success');
        }
    }
}
</script>

<style scoped>

</style>