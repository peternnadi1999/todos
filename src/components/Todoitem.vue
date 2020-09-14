<template>
<div class="todoitem" v-bind:class="{'is-complete':todo.completed}">

    <p>
        <input type="checkbox" v-on:change="markComplete">
        {{todo.title}}
        <button @click="$emit('del-todo',todo.id)" class="del">x</button>
        </p>
</div>
</template>

<script>
export default {
        name:'Todoitem',
        methods:{
            markComplete(){
                this.todo.completed = !this.todo.completed;
            }
        },
        props:["todo"]
    }
</script>

<style scoped>
.todoitem{
    background-color: #f4f4f4;
    padding: 10px;
    border-bottom: 1px dotted #ccc;
}
.is-complete{
    text-decoration: line-through;
}
.del{
    border: none;
    background: #ff0000;
    color:#fff;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
}
.del:hover{
    background: blue;
}
</style>