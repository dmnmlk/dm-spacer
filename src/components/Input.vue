<template>
    <div class="input-wrapper">
      <input
        id="search"
        name="search"
        placeholder="e.g. Moon"
        v-model="inputValue"
        @input="handleInput"
        >
    </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Input',
  data() {
    return {
      inputValue: '',
      apiResponse: [],
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      axios.get(`${API}?q=${this.inputValue}&media_type=image`)
        .then((response) => {
          console.log(response.data.collection.items);

          this.apiResponse = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  .input-wrapper {
    display: flex;
    flex-direction: column;
    width: 250px;

    input {
      color: #FFF;
      border: 0;
      border-bottom: 1px solid #FFF;
      background: none;
      text-align: center;
    }

    input:focus {
      outline: none;
    }

  }
</style>
