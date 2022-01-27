<template>
    <div>
      <h1>Home</h1>
      <transition name="notification">
          <app-notification v-if="showNotification"/> 
      </transition> 
      <app-todos @EmptyInput="handleError"/>
    </div>
</template>

<script>

import Todos from '../components/Todos.vue'
import Notification from '../components/Notification'
import { ref } from '@vue/reactivity'

export default {
    name:'Home',
    components:{
        'app-todos': Todos,
        'app-notification': Notification
    },
    setup(){
        const showNotification = ref(false)
        const show = ref(false)

        const handleError = ()=>{
            showNotification.value = true
            setTimeout(()=>{
                 showNotification.value = false
            },5000)
        }
        
        return{
            handleError, showNotification, show
        }
    }
}
</script>

<style>
   .notification-enter-from{
       transform: translateY(-60px);
       opacity: 0;
   }
   .notification-enter-active{
       transition: all 2s ease;
   }
   .notification-leave-active{
        transition: all 2s ease;
   }
   .notification-leave-to{
       transform: translateY(-60px);
       opacity: 0;
   }
</style>