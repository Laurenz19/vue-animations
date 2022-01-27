<template>
    <div class="todos">
       <input type="text" placeholder="Add a new todo..." v-model="newTodo" @keypress.enter="addTodo">
        <div  v-if="allTodos.length">
            <ul>
                <li v-for="todo in allTodos" :key="todo.id" @click="deleteTodo(todo.id)">
                    {{todo.title}}
                </li>
            </ul>
        </div>
        <div v-else>
            Woohoo, empty todo!
        </div>
    </div>
</template>

<script>
import { ref } from '@vue/reactivity'
export default {
    name:"Todos",
    setup(props, {emit}){
        const newTodo = ref('')
        const allTodos = ref([
            {id:1, title:'learn the basics Vuejs'},
            {id:2, title:'learn annimation in Vuejs'}
        ])

        const addTodo = ()=>{
            let id = Math.random()
            
            if(newTodo.value){
                 allTodos.value.push({id:id, title: newTodo.value})
                 newTodo.value = '' 
            }else{
                emit('EmptyInput')
            } 
        }

        const deleteTodo = (id)=>{
           allTodos.value= allTodos.value.filter((todo)=> todo.id != id)
        }

        return{
            newTodo, allTodos, addTodo, deleteTodo
        }
    }
}
</script>

<style>
    .todos{
        max-width: 400px;
        margin:20px auto;
        position: relative;
    }

    input{
        width: 100%;
        padding: 12px;
        border:1px solid #eee;
        border-radius: 10px;
        box-sizing: border-box;
        margin-bottom: 20px
    }

    .todos ul{
        position: relative;
        padding: 0;
    }

    .todos li{
        list-style-type: none;
        display: block;
        margin-bottom: 10px;
        padding: 10px;
        background: white;
        box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
        border-radius: 10px;
        width: 100%;
        box-sizing: border-box;
    }

    .todos li:hover{
        cursor: pointer;
    }
</style>