<script setup>
import { defineProps, ref } from 'vue';

let props = defineProps({
    mobile : Boolean
})
let clicked = ref(false)

</script>

<template>
<nav class="mobile_navbar" v-if="mobile">
    <div class="dropdown" ><i class="fa-solid fa-bars fa-xl" @click="clicked = !clicked"></i>
        <ul class="dropdown_content" v-if="clicked">
            <li><i class="fa-solid fa-xmark fa-xl" @click="clicked = false"></i></li>
            <li>Home</li>
            <li>Shop</li>
            <li>About</li>
            <li>Contact</li>
        </ul>
    </div>
    <h1>room</h1>
    
</nav>
<nav class="desktop_navbar" v-else>
    <h1>room</h1>
    <ul>
        <li>home</li>
        <li>shop</li>
        <li>about</li>
        <li>contact</li>
    </ul>
</nav>
</template>

<style lang="scss">
.mobile_navbar{
    position: absolute;
    width: 100vw;
    color: white;
    padding: 1rem 0 0 2rem;
    z-index: 1;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: start;
    h1{
        width: 70%;
        font-size: 1.7rem;
        text-align: center;
    }
    .dropdown{
        box-sizing: border-box;
        .dropdown_content{
            list-style: none;
            display: flex;
            position:absolute;
            justify-content: space-evenly;
            align-items: center;
            background-color: white;
            color: black;
            font-size: 1.2rem;
            font-weight: bolder;
            top: 0;
            height: 10vh;
            left: 0;
            margin: 0;
            padding: 0;
            width: 100vw;
        }
    }
    
}

</style>