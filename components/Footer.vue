<template>
<footer>
  <div class="container flex-row justify">
    <n-link :to="link.back" class="link link__left">{{ $t('btn.contactUs') }}</n-link>
    <n-link :to="link.forward" class="link link__right" :class="{light: light}">{{$t('btn.more')}}</n-link>
  </div>
</footer>
</template>

<script>
export default {
  props: ['link', 'light'],
  name: "Footer"
}
</script>

<style lang="scss" scoped>
@import "assets/components/colors";
footer {
  position:absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding-bottom: 3rem;
  .link{
    color:  $secondary_color;
    text-decoration: none;
    position: relative;
    transition: all 400ms ease-in-out;
    &::before{
      position: absolute;
      content:'';
      top: 50%;
      width: 3rem;
      background: $secondary_color;
      height: 1px;
      transition: width 400ms ease-in-out;
    }
    &__left{
      padding-left: 3.5rem;
      &::before{
        left: 0;
      }
      &:hover {
        padding-left: 6.5rem;
        &::before {
          width: 6rem;
        }
      }
    }
    &__right{

      padding-right: 3.5rem;
      &::before{
        right: 0;
      }
      &:hover{
        padding-right: 6.5rem;
        &::before {
          width: 6rem;
        }
      }
    }
  }
  & .light{
    color: $light_color;
    &::before{
      background: $light_color;
    }
  }
}
</style>
