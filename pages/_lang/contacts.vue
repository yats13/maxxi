<template>
<main class="contacts">
  <div class="container flex-column">
    <section class="clients__wrapper">
      <h1>{{ $t('contactsTitle1') }}</h1>
      <div class="flex-row">
        <div class="clients">
          <div class="grid">
            <div class="client" v-for="client in images">
              <img :src="client.pathLong" :alt="client.pathShort">
            </div>
          </div>
        </div>
        <div class="block__red flex-column">
          <div class="title__wrapper">
            <h2 class="white">{{ $t('toBeClient') }}</h2>
          </div>
          <div class="content__wrapper">
          <p v-for="(stepItem, index) in $t('contacts.steps')"
             :key="index"
             class="white steps"
             v-if="step >= (index + 1)"
          >
            {{ stepItem }}
          </p>
          </div>
        <nav class="numbers flex-row">
          <a v-for="number in $t('contacts.steps').length"
             class="number"
             v-if="number <= step + 1"
             @click.prevent="step = number"
             :class="{ active: step >= number }"
             :key="number"
          >
            {{number}}
          </a>
        </nav>
        </div>
      </div>
    </section>
    <section>
      <h1>{{ $t('contactsTitle2') }}</h1>
      <div class="flex-row">
        <div class="block__red flex-row justify-around">
          <div class="address">
            <h2 class="white">{{$t('addressTitle')}}</h2>
            <p class="white">Украина,<br>
              01054, г. Киев <br>
              ул. Дмитриевская, 52-б, оф 1</p>
          </div>
          <div class="vertical-line"></div>
          <div class="phone">
            <h2 class="white">{{$t('phoneTitle')}}</h2>
            <p class="white">
              email: sshmorgun@aamc.com.ua, <br>
              телефоны: 0674474812, 0674474815<br> факс +38 044 228-52-41
            </p>
          </div>
        </div>
        <div class="block__right">
          <form class="flex-column"
                @submit="checkForm"
          >
            <div class="flex-row">
              <span class="col-50">
                <input v-model="selected.name" id="name" type="text">
                <label for="name"
                :class="{active: labelNotEmpty(selected.name)}"
                >Имя</label>
              </span>
              <span class="col-50">
                <select v-model="selected.service">
                  <option disabled :value="$t('services').length">{{ $t('btn.option') }}</option>
                  <option v-for="(service, index) in $t('services')" :value="index">{{service.title}}</option>
                </select>
              </span>
            </div>
            <div class="flex-row">
              <span class="col-50">
                <input v-model="selected.phone" id="phone" type="tel" pattern="\([0-9]{3}\)[0-9]{3}-[0-9]{2}-[0-9]{2}">
                <label for="phone"
                       :class="{active: labelNotEmpty(selected.phone)}"
                >
                  {{ $t('phoneTitle') }}
                </label>
              </span>
              <span class="col-50">
                <input v-model="selected.email" id="email" type="email">
                <label for="email"
                       :class="{active: labelNotEmpty(selected.email)}"
                >
                  E-mail
                </label>
              </span>
            </div>
            <button
              type="submit"
              class="btn"
            >{{ $t('btn.send') }}</button>
          </form>
        </div>
      </div>
    </section>
  </div>
  <v-modal v-if="checkForm" />
</main>
</template>

<script>
import VModal from '@/components/Modal'
export default {
  name: "contacts",
  components:{
    VModal
  },
  data(){
    return{
      images:[],
      selected:{
        service: this.$t('services').length
      },
      step: 1,
    }
  },
  mounted() {
    this.importAll(require.context('@/assets/images/clients/', true, /\.png$/));
  },
  methods: {
    importAll(r) {
      r.keys().forEach(
        key => (
          this.images.push({
            pathLong: r(key), pathShort: key
          })
        )
      );
    },
    labelNotEmpty(message){
      if(message === '' || message === null || message === undefined){
        return false;
      } else {
        return true;
      }
    },
    checkForm: function (e) {
      if (
        this.selected.forEach(key => this.labelNotEmpty(key))) {
        return true;
      }

      this.errors = [];

      if (!this.selected.name) {
        this.errors.push('Требуется указать имя.');
      }
      if (!this.selected.email) {
        this.errors.push('Требуется указать email.');
      }

      e.preventDefault();
    }
  }
}
</script>

<style lang="scss" scoped>
@import "assets/common";
.contacts{
  flex: 4 4 calc(100% - 5rem);
  section{
    flex: 1 1 50%;
  }
}
.clients{
  display: grid;
  flex: 1 1 50%;
  align-items: center;
  &__wrapper{
    display: flex;
    flex-wrap: wrap;
  }
  img{
    object-fit: contain;
    max-width: 100%;
    max-height: 6rem;
    padding: 1rem;
  }
}
.vertical-line{
  height: 80%;
  margin: 2rem;
  width: 1px;
  background: $light_color;
  @media screen and (max-width: 1050px) {
    height: 1px;
    width: 80%;
  }
}
.numbers{
  justify-content: center;
  margin: 2rem 0;
  flex-wrap: nowrap;
  .number{
    display: block;
    color: $light_color;
    background:$secondary_color;
    height: 2rem;
    width: 2rem;
    border-radius: 50%;
    border: 2px solid $light_color;
    text-align: center;
    margin-left: 3rem;
    position: relative;
    box-shadow: 0 0 0 0 rgba(255, 255, 255, 1);
    transform: scale(1);
    animation: pulse 2s infinite;
    &.active, &:hover {
      animation: none;
      background: $light_color;
      color: $secondary_color;
      &::before {
        content: '';
        position: absolute;
        background: $light_color;
        width: 4rem;
        height: 1px;
        left: -4rem;
        top: 50%;
        transform: translateY(-50%);
      }
    }
    &:hover::before{
      animation-name: numbers;
      animation-duration: 1s;
    }
    &:nth-child(1){
      margin-left: 0;
      &::before{
        display: none;
      }
    }
  }
}
form{
  margin: 2rem auto;
  width: 80%;
  span{
    display: block;
    position: relative;
    label{
      position: absolute;
      color: $header_color;
      left: 0;
      top: 0;
      z-index: 3;
      transition: all 300ms ease-in;
      &.active{
        top:-1em;
        font-size: 80%;
      }
    }
    input{
      padding: .5rem 0;
      width: 90%;
      margin-bottom: 3rem;
      border: none;
      border-bottom: 1px solid $header_color;
      &:focus + label{
        top:-1em;
        font-size: 80%;
      }
    }
  }
}
.steps{
  line-height: 1.5;
  font-size: 1.25em;
}
@keyframes numbers {
  from{
    background: transparent;
    transform: translateX(-50%);
  }
  to{
    background: $light_color;
    transform: translateX(0);
  }
}

@keyframes pulse {
  0% {
    transform: scale(0.95);
    box-shadow: 0 0 0 0 rgba(255, 255, 255, 0.7);
  }

  70% {
    transform: scale(1);
    box-shadow: 0 0 0 10px rgba(255, 255, 255, 0);
  }

  100% {
    transform: scale(0.95);
    box-shadow: 0 0 0 0 rgba(255, 255, 255, 0);
  }
}
</style>
