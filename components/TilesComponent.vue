<template>
  <div class="tile">
    <div class="overlay">
      <div class="overlay-info">
        <p class="name">{{ item.id }}</p>
        <p class="desc">{{ item.alt_description }}</p>
      </div>
    </div>

    <div class="tile-icon">
      <img src="../assets/icons/chevron-right.svg" alt="chevron right" />
    </div>
    <img
      class="tile-img"
      :src="item.urls.regular"
      :alt="item.alt_description" width="20" height="20"
    />
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
  position: relative;
  transition: all 0.4s ease;

  &:hover {
    .overlay {
      visibility: visible;
      opacity: 1;
      height: 100%;
    }
  }

  &-img {
    width: 100%;
    height: 100%;
    display: block;
    object-fit: cover;
  }
}

.overlay {
  position: absolute;
  width: 100%;
  height: 0%;
  top: 0;
  left: 0;
  background: #4a52ff;
  cursor: pointer;
  visibility: hidden;
  opacity: 0;
  transition: all 0.4s ease-in-out;
  padding: 1rem;

    .name {
      font-size: 0.875rem;
      text-transform: uppercase;
      line-height: 2;
      font-weight: bold;
    }

    .desc {
      font-size: .857rem;
      text-transform: capitalize;
    }

}

.tile-icon {
  position: absolute;
  bottom: 1.25rem;
  right: 1.25rem;
}
</style>
