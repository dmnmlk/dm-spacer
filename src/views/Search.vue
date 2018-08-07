<template>
  <div class="wrapper">
    <Claim />
    <Input />
    <ul>
      <!-- <div v-for="item in apiResponse" :key="item.data[0].nasa_id">
        <div>{{item.links[0].href}}</div>
        <div>{{item.data[0].description}}</div>
      </div> -->
    </ul>
  </div>
</template>

<script>

import Claim from '@/components/Claim.vue';
import Input from '@/components/Input.vue';


export default {
  name: 'Home',
  components: {
    Claim,
    Input,
  },
};
</script>

<style lang="scss" scoped>

  body {
    margin: 0;
    padding: 0;
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
    background-image: url("../assets/heroimage.jpg");
    background-size: cover;
    background-position: 80% 0%;
  }
</style>
