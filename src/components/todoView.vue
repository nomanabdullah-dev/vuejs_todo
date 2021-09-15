<template>
    <div>
        <div v-for="(todo, index) in todos" :key="index">
            <list-todo 
            :todo="todo"
            class="todo"
            v-on:todoChanged="$emit('reloadTodo')" />
        </div>
    </div>
</template>

<script>
import listTodo from './listTodo.vue'
    export default {
        props: ['todos'],
        components: { listTodo }
    }
</script>

<style scoped>
.todo{
    background: #e6e6e6;
    padding: 5px;
    margin-top: 5px;
}
</style>