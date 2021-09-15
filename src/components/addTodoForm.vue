<template>
    <div class="addTodo">
        <input type="text" v-model="task.title">
        <i class="fa fa-plus-square" :class="[ task.title ? 'active':'inactive', 'plus']" @click="addTodo()"></i>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        data() {
            return {
                task: {
                    title: ''
                }
            }
        },
        methods: {
            addTodo() {
                if(this.task.title == ''){
                    return;
                }
                axios.post('http://127.0.0.1:3333/todo', {
                    title: this.task.title
                })
                .then(response => {
                    if(response.status == 201) {
                        this.task.title = ''
                        this.$emit('todoChanged')
                    }
                })
                .catch(error => {
                    console.load( error)
                })
            }
        },
    }
</script>

<style scoped>
.addTodo{
    display: flex;
    justify-content: center;
    align-items: center;
}
input{
    background: #f7f7f7;
    border: 0px;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
}
.plus{
    font-size: 20px;
}
.active{
    color: #00CE25;
}
.inactive{
    color: #999999;
}
</style>