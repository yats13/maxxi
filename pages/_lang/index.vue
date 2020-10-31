<template>
    <div class="slider">
      <div class="slider__image">
        <transition name="slide-fade">
        <div class="slide"
             :style="{
                backgroundImage: 'url('+ require('@/assets/images/'+ images[currentImage] ) +')'
             }"
             :key="currentImage"
        >
        </div>
        </transition>
      </div>
      <div class="slider__footer">
        <div class="flex-row">
          <div class="slider_text__wrapper">
            <transition name="flip" mode="out-in">
            <div class="slider_text" :key="currentSlide">
              <h1 :key="currentSlide">{{slide.title}}</h1>
              <p v-html="slide.description" class="description"></p>
            </div>
            </transition>
            <nav class="slider_nav">
              <a v-for="item in $t('index').length"
                 :key="item"
                 @click="setSlider(item)"
                 class="dot"
                 :class="{dot__active: currentSlide === item}"
              ></a>
            </nav>
          </div>
          <div class="right_block">
            <h2 class="white">КОМПЕТЕНЦИИ</h2>
            <p class="white">Мы реализуем проекты во всех возможных каналах коммуникации в Украине и за ее пределами</p>
          </div>
          <vue-footer :link="link" light="true"/>
        </div>
      </div>
    </div>
</template>

<script>
import Logo from '@/components/Logo.vue'
import VueFooter from "@/components/Footer"
import axios from 'axios'
export default {
  components: {
    Logo, VueFooter
  },
  data(){
    return {
      currentSlide: 1,
      currentImage: 0,
      slide: this.$t(`index[0]`),
      link: {
        back: "contacts",
        forward: "competentions"
      },
      images:[
        "brooke-cagle--uHVRvDr7pg-unsplash-min.jpg",
        "s-o-c-i-a-l-c-u-t-kAyZO7V9MUs-unsplash-min.jpg",
        "ron-dyar-V29UWcALNko-unsplash-min.jpg"
      ]
    }
  },
  computed:{
    changeCurrentSlide: {
      get(){
        return this.currentSlide
      },
      set(val){
        this.currentSlide = val > this.$t('index').length ? 1 : val
      }
    }
  },
  mounted(){
    setInterval(() => {
      this.changeCurrentSlide++
      this.setSlider(this.currentSlide)
    },3000)
  },
  methods:{
    setSlider(val) {
      this.changeCurrentSlide = val
      this.currentImage = this.currentSlide -1
      this.slide = this.$t(`index[ ${this.currentImage}]`)
    }
  }
}
</script>

<style lang="scss">
@import "assets/common";
.slider{
  display: flex;
  height: calc(100% - 6rem);
  flex-direction: column;
  justify-content: space-between;
  &__image{
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    height: 100%;
    max-width: 100%;
    z-index: -1;
  }
  &__footer{
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
  }
  .slide{
    width: 100%;
    height: 72vh;
    background-size: cover;
  }
  .flex-row{
    align-items: flex-end;
    position: relative;
  }
  &_text {
    &__wrapper {
      width: 50%;
      max-width: $width / 2;
      padding: 5%;
      background-color: #fff;
      box-shadow: 10px 0px 25px rgba(0, 0, 0, 0.25);
    }
  }
}
.right_block{
  background-color: $secondary_color;
  flex: 1;
  height: 18 * $size;
  padding: 5%;
}
.slider_nav {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin: 2rem 0;
  .dot{
    margin-right: .5rem;
    display: block;
    height: .4rem;
    width: .4rem;
    background-color: $header_color;
    border-radius: 50%;
    &__active {
      background-color: $secondary_color;
    }
  }
}
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
  /* .slide-fade-leave-active до версии 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}

.flip-enter-active {
  transition: all .3s cubic-bezier(0.55, 0.085, 0.68, 0.53); //ease-in-quad
}

.flip-leave-active {
  transition: all .35s cubic-bezier(0.25, 0.46, 0.45, 0.94); //ease-out-quad
}

.flip-enter, .flip-leave-to {
  transform: scaleY(0) translateZ(0);
  opacity: 0;
}

</style>
