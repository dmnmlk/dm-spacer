<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input
        id="search"
        name="search"
        placeholder="e.g. Moon"
        v-model="inputValue"
        @input="handleInput"
        >
    </div>
    <ul>
      <div v-for="item in apiResponse" :key="item.data[0].nasa_id">
        {{item.links[0].href}}
      </div>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Home',
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
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
  }

  .search {
    display: flex;
    flex-direction: column;
    width: 250px;

    label {
      margin-bottom: 5px;
    }

    input {
      border: 0;
      border-bottom: 1px solid #000;
    }

    input:focus {
      outline: none;
    }

  }
</style>
