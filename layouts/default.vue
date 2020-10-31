<template>
  <div class="wrapper">
    <header>
      <div class="container flex-row justify">
        <button @click="isActive=!isActive"
                :class="[isActive? 'services_btn__active': 'services_btn']"
        >
          <div class="toggle flex-column">
            <span class="line line1"></span>
            <span class="line line2"></span>
            <span class="line line3"></span>
          </div>
          <span v-if="isActive">
            {{$t('close')}}
          </span>
          <span v-else>
            {{$t('serviceTitle')}}
          </span>
        </button>
        <vue-logo />
        <div class="lang-dropdown">
          <NuxtLink v-if="$i18n.locale === 'ru'" :to="`/en` + $route.fullPath" class="Header__Link" active-class="none" exact>
            En
          </NuxtLink>
          <NuxtLink v-else :to="$route.fullPath.replace(/^\/[^\/]+/, '')" class="Header__Link" active-class="none" exact>
            Ru
          </NuxtLink>
        </div>
      </div>
    </header>
    <nuxt />
    <transition name="slide-fade">
      <vue-menu v-if="isActive" />
    </transition>
  </div>
</template>
<script>
import Logo from '@/components/Logo'
import Menu from '@/components/Menu'
export default {
  components:{
    vueLogo: Logo,
    vueMenu: Menu
  },
  data(){
    return{
      isActive: false
    }
  }
}
</script>
<style lang="scss" scoped>
  @import "assets/common";
  header{
    z-index: 101;
  }
  .toggle {
    justify-content: space-evenly;
    margin-right: $margin;
    .line {
      display: block;
      width: 1rem;
      height: 2px;
      background-color: $header_color;
      transition: 0.2s transform ease-out;
    }
    .line2{
      background-color: $secondary_color;
    }
  }
  .services_btn{
    text-transform: uppercase;
    font-weight: 600;
    color: $header_color;
    display: flex;
    &__active{
      text-transform: uppercase;
      font-weight: 600;
      color: $header_color;
      display: flex;
      .toggle{
        justify-content: center;
        align-items: center;
      }
      .line3{
        display: none;
      }
      .line1{
        transform: rotate(-45deg) translateX(-1px);
      }
      .line2{
        transform: rotate(45deg) translateX(-1px);
      }
    }
  }
  .lang-dropdown a{
    color: $header_color;
    text-decoration: none;
    font-weight: 600;
  }
</style>
