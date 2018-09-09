<template>
    <div class="input-wrapper">
      <input
        id="search"
        name="search"
        :class="{ dark }"
        placeholder="e.g. Moon"
        :value="value"
        @input="handleChange"
        >
    </div>
</template>

<script>
export default {
  name: 'Input',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
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
      box-shadow: 0px 15px 15px -5px rgba(255, 255, 255, .2);
    }

    .dark {
      color: #1e3d4a;
      border-bottom: 1px solid #1e3d4a;

    }

    ::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
        color: #CCC;
        opacity: 1; /* Firefox */
    }

    :-ms-input-placeholder { /* Internet Explorer 10-11 */
        color: #CCC;
    }

    ::-ms-input-placeholder { /* Microsoft Edge */
        color: #CCC;
    }

  }
</style>
