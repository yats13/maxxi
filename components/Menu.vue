<template>
  <section class="menu">
    <div class="container">
    <h1>{{ $t('serviceTitle') }}</h1>
      <div class="service_list__wrapper grid">
        <div v-for="(item, index) in $t('services')"
            :key="index"
            @mouseover="hover = index"
            @mouseleave="hover = null"
            class="service_list__item"
        >
          <h2>{{ item.title }}</h2>
          <ul class="service_list">
            <li v-for="service in item.description">{{service}}</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Menu",
  data() {
    return {
      hover: null,
    };
  }
}
</script>

<style scoped lang="scss">
@import "assets/common";
.menu{
  position: absolute;
  width: 100%;
  background-color: #fff;
  z-index: 100;
  height: 100%;
  .container{
    margin-top: 6rem;
  }
}
.service_list {
  &__wrapper{
    display: grid;
    gap: 1rem;
    grid-template-columns: repeat( auto-fit, minmax(280px, 1fr) );
  }
  &__item {
    border: 1px solid $light_color;
    padding: 3rem;
  }
}
</style>
