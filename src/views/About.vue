<template>
    <div class="about">
        <transition name="fade"
        appear
        @before-enter="beforeEnter"
        @enter="enter"
        @after-enter="afterEnter"
        @before-leave="beforeLeave"
        @leave="leave"
        @after-leave="afterLeave"
        >
             <h1 v-show="showTitle">About</h1>
        </transition>
      
       <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quos similique fugit necessitatibus architecto dolor dolores ipsam earum ullam vel? Eaque soluta tempora vero voluptas reprehenderit quia voluptatum delectus quaerat asperiores?</p>
       <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Iste suscipit ipsam dolore cum reprehenderit error facilis consectetur libero beatae. Libero incidunt dolores ratione. Quisquam, expedita. Neque deleniti debitis quas! Voluptatum!</p>
       <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Dolore perferendis, repudiandae voluptatibus dignissimos sequi vero magni doloremque quidem possimus itaque accusantium, nulla maxime, corporis distinctio quos commodi eveniet? Distinctio, fugiat.</p>
    </div>
</template>

<script>
import { ref } from '@vue/reactivity'

export default {
    name:'About',
    setup(){
        let showTitle = ref(true)
        const beforeEnter= (el) => {
            console.log("beforeEnter", el);
        }

        const enter =(el)=>{
            console.log("Enter", el);
        }

        const afterEnter = (el)=>{
            console.log("afterEnter", el);
            el.style.color = 'pink '
            setTimeout(()=>showTitle.value = false, 3000)
        }

        const beforeLeave = (el)=>{
             console.log("beforeEnter", el);
        }

        const leave = (el)=>{
             console.log("leave", el);
        }

        const afterLeave = (el)=>{
             console.log("afterLeave", el);
        }
        return {
            beforeEnter, enter, afterEnter, beforeLeave, leave, afterLeave, showTitle
        }
    }
}
</script>

<style>
    .about p{
        max-width: 600px;
        margin:20px auto;
        text-align: justify;
    }
    
    .fade-enter-from, .fade-leave-to{
        opacity: 0;
    }

    .fade-enter-active{
        transition: all 8s ease;
    }

    .fade-leave-active{
        transition: all 8s ease;
    } 

</style>