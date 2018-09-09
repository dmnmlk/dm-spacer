<template>
    <div class="heroImage" />
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style lang="scss" scoped>
    .heroImage {
        position: fixed;
        z-index: -1;
        width: 100%;
        height: 100vh;
        background-image: url("../assets/heroimage.jpg");
        background-size: cover;
        background-position: 90% 100%
    }

    .heroImage::after {
        position: absolute;
        background: rgba(0,0,0, .3);
        content: '';
        top: 0;
        left: 0;
        z-index: 1;
        width: 100%;
        height: 100vh;
    }
</style>

