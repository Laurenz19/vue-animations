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

    /* Custom animations */
    @keyframes shake {
       0%{
           transform: translateY(-60px);
           opacity: 0; 
       }
       50%{
           transform: translateY(5 px);
           opacity: 1;
       }
       60%{transform: translateX(8px);}
       70%{transform: translateX(-8px);}
       80%{transform: translateX(4px);}
       90%{transform: translateX(-4px);}
       100%{transform: translateX(0px);}
   }
    
   /* Enter Classes */ 
   /*.notification-enter-from{
       transform: translateY(-60px);
       opacity: 0;
   }*/
   .notification-enter-active{
       animation: shake 0.5s ease;
   }

   /* Leave classes*/
   .notification-leave-active{
        transition: all 2s ease;
   }
   .notification-leave-to{
       transform: translateY(-60px);
       opacity: 0;
   }
</style>