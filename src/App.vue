<script setup>
import  NavBar  from './components/NavBar.vue'
import { ref } from 'vue'

let image_information = [
  {
    src : "src/assets/mobile-image-hero-1.jpg",
    title : "Discover innovative ways to decorate",
    text : `We provide unmatched quality, comfort, and style for property owners across the country. 
            Our experts combine form and function in bringing your vision to life. Create a room in your 
            own style with our collection and make your property a reflection of you and what you love.`
  },
  {
    src : "src/assets/mobile-image-hero-2.jpg",
    title : "We are available all across the globe",
    text : `With stores all over the world, it's easy for you to find furniture for your home or place of business. 
            Locally, we’re in most major cities throughout the country. Find the branch nearest you using our 
            store locator. Any questions? Don't hesitate to contact us today.`
  },
  {
    src : "src/assets/mobile-image-hero-3.jpg",
    title : " Manufactured with the best materials",
    text : `Our modern furniture store provide a high level of quality. Our company has invested in advanced technology 
            to ensure that every product is made as perfect and as consistent as possible. With three decades of 
            experience in this industry, we understand what customers want for their home and office.`
  } 
]
let device_size = ref(window.innerWidth)
let image_id = ref(0)
let UserSwipe = ref({
  start : null,
  end : null
})
let handleNext =()=> image_id.value<2? image_id.value +=1 : image_id.value=0

let handlePrevius = () => image_id.value>0 ? image_id.value -=1 : image_id.value=2

let handleTouchEnd = (event) =>{
  if(UserSwipe.value.start && UserSwipe.value.end){
    let distance = UserSwipe.value.start - UserSwipe.value.end
    if(distance > 50){
      handleNext()
    }
    else if(distance<-50){
      handlePrevius()
    }
  }
}


</script>
<template>
 <div class="main_container" >
  <NavBar :mobile="device_size>= 800? false : true"/>
  <section class="home">
    <img alt="home product image" :src="image_information[image_id].src" @touchstart="UserSwipe = {...UserSwipe, start : $event.touches[0].clientX}" @touchmove="UserSwipe = {...UserSwipe, end : $event.touches[0].clientX} " @touchend="handleTouchEnd" class="home_image">
    <div class="button_slide">
      <button aria-pressed="Previus picture" @click="handlePrevius" ><i class="fa-solid fa-caret-left fa-2xl"></i></button>
      <button aria-pressed="Next picture" @click="handleNext"><i class="fa-solid fa-caret-right fa-2xl"></i></button>
    </div>
    <div class="home_content">
      <h1>{{ image_information[image_id].title }}</h1>
      <p>{{ image_information[image_id].text }}</p>
      <h2>Shop Now <i class="fa-solid fa-arrow-right-long fa-xl"></i></h2>
    </div>
  </section>
  <section class="about">
    <figure>
      <img alt="about start image description" src="./assets/image-about-dark.jpg">
    <figcaption>
      <h3>About our furniture</h3>
      <p>Our multifunctional collection blends design and function to suit your individual taste.
        Make each room unique, or pick a cohesive theme that best express your interests and what
        inspires you. Find the furniture pieces you need, from traditional to contemporary styles
        or anything in between. Product specialists are available to help you create your dream space.
      </p>
    </figcaption>
    <img alt="about end image description" src="./assets/image-about-light.jpg">
    </figure>
  </section>
  </div>
</template>

<style lang="scss">

@import "@fortawesome/fontawesome-free/css/all.css";
.main_container{
  min-width: 100vw;
}

.home{
  img{
    width: 100%;
  }
  .button_slide{
    display: flex;
    justify-content: center;

    button{
      border: none;
      color: white;
      background-color: hsl(0, 0%, 0%);
      width: 3rem;
      height: 3rem;
      border-radius: 5%;
      &:active{
        background-color: hsl(0, 0%, 27%);
      }
    }
  }
  .home_content{
    padding: 1rem 0 1rem 0;
    width: 80%;
    margin: auto;
    h1{
      font-size: 2rem;
    }
    p{
      font-size: 1rem;
      color: grey;
      letter-spacing: 1px;
    }
    h2{
      display: flex;
      align-items: center;
      gap: 1rem;
      font-size: 1.8rem;
      &:hover{
        color: hsl(0, 0%, 27%);
      }
    }
  }
}
.about{
  figure{
    width: 100%;
    margin: 0;
  }
  img{
    width: 100%;
    object-fit: cover;
  }
  figcaption{
    padding: 1rem 0 2rem 0;
    width: 80%;
    margin: auto;
    h3{
      font-size: 1.5rem;
      letter-spacing: 1px;
    }
    p{
      font-size: 1rem;
      color: grey;
      letter-spacing: 1px;
    }
  }
}
.main_container:has(.dropdown_content){
  background-color: rgba(0,0,0,.85);
  img{
    opacity: .30;
  }
}


</style>
