<template>
  <div class="tile">
    <img class="tile-img" :src="item.urls.regular" :alt="item.alt_description">
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: false,
      default() {
        return {}
      },
    },
  },
}
</script>

<style lang="scss" scoped>
.tile {
  margin: 0;
  // background-repeat: no-repeat;
  // background-size: cover;
  // background-position: top;

  &-img {
    width: 100%;
    height: 100%;
    display: block;
    object-fit: cover;
  }

}
</style>
