<template>
    <div class="todos">
       <input type="text" placeholder="Add new todo..." v-model="newTodo" @keypress.enter="addTodo">
        <transition name="switch" mode="out-in">
        <div  v-if="allTodos.length">
            <transition-group tag="ul" name="todo-list" appear>
                <li v-for="todo in allTodos" :key="todo.id" @click="deleteTodo(todo.id)">
                    {{todo.title}}
                </li>
            </transition-group>
        </div>
        <div v-else>
            Woohoo, empty todo!
        </div>
        </transition>
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

    /* Custom animation */
    @keyframes adding-todo {
        0%{transform: scale(0.6); opacity: 0;}
        100%{ transform: scale(1); opacity: 1;}
    }

    /* Todo list transition */

    /* Enter */
    .todo-list-enter-active{
        animation: adding-todo 0.5s ease;
    }

    /* Leave*/
    .todo-list-leave-active{
        animation: all 0.1s ease;
        position: absolute;
    }
    .todo-list-leave-to{
        opacity: 0;
    }

    .todo-list-move{
        transition: all 0.5s ease;
    }

    /* Swicth animation */
    .switch-enter-from, .switch-leave-to{
       transform: translateY(20px);
        opacity:  0;
    }
    .switch-enter-to, .switch-leave-from {
        transform: translateY(0px);
        opacity:  1;
    }
    .switch-enter-active{
        transition: all 0.4s ease;
    }
   
    .switch-leave-active{
       transition: all 0.4s ease;
    }

</style>