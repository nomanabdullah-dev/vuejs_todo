<template>
    <div class="todo">
        <input 
            type="checkbox"
            @change="updateCheck()"
            v-model="todo.is_completed" 
        />
        <span :class="[todo.is_completed ? 'completed':'', 'todoText']">{{ todo.title }}</span>
        <button @click="removeTodo()" class="trash"><i class="fa fa-trash"></i></button>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        props: ['todo'],
        methods: {
            updateCheck() {
                axios.put('todo/' + this.todo.id, {
                    todo: this.todo
                })
                .then( response => {
                    if(response.status == 200) {
                        this.$emit('todoChanged')
                    }
                })
                .catch(error => {
                    console.log(error)
                })
            },
            removeTodo() {
                axios.delete('todo/' + this.todo.id)
                .then( response => {
                    if(response.status == 200) {
                        this.$emit('todoChanged')
                    }
                })
                .catch(error => {
                    console.log(error)
                })
            }
        },
    }
</script>

<style scoped>
.completed{
    text-decoration: line-through;
    color: #999999;
}
.todoText{
    width: 100%;
    margin-left: 20px;
}
.todo{
    display: flex;
    justify-content: center;
    align-content: center;
}
.trash{
    background: #e6e6e6;
    border: none;
    color: #FF0000;
    outline: none;
}
</style>