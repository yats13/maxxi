<template>
<section class="competentions">
  <div class="container flex-column">
    <h1>{{ $t('competentionTitle') }}</h1>
    <div class="service_list__wrapper">
      <div v-for="(item, index) in $t('competenions')"
           :key="index"
           @mouseover="hover = index"
           @mouseleave="hover = null"
           class="service_list__item"
      >

         <h2>{{ item.title }}</h2>
        <div class="flex-row inside">
         <ul class="service_list">
           <li v-for="service in item.description">{{service}}</li>
         </ul>
        <img :src="require('@/assets/images/competentions/' + item.image)" alt="" width="120">
        </div>
      </div>
    </div>
  </div>
  <vue-footer :link="link"/>
</section>
</template>

<script>
import VueFooter from "@/components/Footer"
export default {
  name: "competentions",
  components:{
    VueFooter
  },
  data(){
    return{
      link:{
        forward:"contacts",
        back:"/"
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import "assets/components/colors";
.service_list {
  &__wrapper{
    display: grid;
    gap: 1rem;
    grid-template-columns: repeat( auto-fit, minmax(280px, 1fr) );
    justify-content: center;
    margin: 0 auto;
    @media screen and (max-width: 1440px) {
      max-width: 960px;
    }
  }
  &__item{
    border: 1px solid $light_color;
    padding: 1rem 2rem;
    img{
      object-fit: contain;
    }
    .inside{
      justify-content: space-around;
      align-items: center;
      flex-wrap: nowrap;
    }
  }
}
</style>
