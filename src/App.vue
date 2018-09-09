<template>
  <div :class="[{flexStart: step === 1}, 'wrapper']">
    <transition name="slide">
    <img class="logo" src="./assets/logo.svg" v-if="step === 1"/>
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <Input
      class="input"
      v-model="inputValue"
      @input="handleInput"
      :dark="step === 1" />
    <div
      class="results"
      v-infinite-scroll="loadMore"
      infinite-scroll-disabled="busy"
      v-if="apiResponse && !loading && step === 1">
      <Item v-for="item in apiResponse" :item="item" :key="item.data[0].nasa_id"/>
    </div>
  </div>

</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import Input from '@/components/Input.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import infiniteScroll from 'vue-infinite-scroll';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',
  directives: { infiniteScroll },
  components: {
    Claim,
    Input,
    HeroImage,
    Item,
  },
  data() {
    return {
      loading: false,
      step: 0,
      inputValue: '',
      apiResponse: [],
      busy: false,
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API}?q=${this.inputValue}&media_type=image`)
        .then((response) => {
          this.apiResponse = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
    loadMore: () => {
      console.log('siemanko');
      this.busy = true;
      setTimeout(() => {
        axios.get(`${API}?q=${this.inputValue}&media_type=image`)
          .then((response) => {
            this.apiResponse.push(response.data.collection.items);
          })
          .catch((error) => {
            console.log(error);
          });
        this.busy = false;
      }, 1000);
    },
  },
};
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

  $font-weight-light: 300;
  $font-weight-normal: 400;
  $font-weight-bold: 600;
  $font-weight-black: 800;

  * {
    box-sizing: border-box;
  }
  body {
    font-family: 'Montserrat', sans-serif;
    margin: 0;
    padding: 0;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity .3s ease;
  }

  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active,
  .slide-leave-active {
    transition: margin-top .3s ease;
  }

  .slide-enter,
  .slide-leave-to {
    margin-top: -50px;
  }

  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    height: 100vh;

    &.flexStart {
      justify-content: flex-start;
    }

    .logo {
      position: relative;
    }

    .input {
      padding-top: 20px;
    }

    .results {
      width: 100%;
      padding-top: 100px;
      display: grid;
      grid-template-columns: 1fr;
      grid-gap: 20px;

      @media (min-width: 768px) and (max-width: 1023px) {
        grid-template-columns: 1fr 1fr;
      }

      @media (min-width: 1024px) {
        grid-template-columns: 1fr 1fr 1fr;
      }
    }
  }
</style>
