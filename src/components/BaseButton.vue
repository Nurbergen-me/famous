<template>
    <button class="btn cart" v-if="loading">
        <img class="btn__loader" src="/assets/circle-loader.gif">
    </button>
    <button class="btn cart" v-else-if="inCart">
        <img src="/assets/check-icon.svg" alt="check">
        В корзине
    </button>
    <button class="btn" v-else>
        <slot />
    </button>
</template>

<script setup>
const props = defineProps(['loading','inCart'])
</script>

<style lang="scss" scoped>
.btn {
  height: 48px;
  width: 122px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  background: #403432;
  color: #fff;
  font-size: 14px;
  font-weight: 700;
  cursor: pointer;
  transition: 0.5s ease;

  &:hover {
    background: #776763;
  }

  &__loader {
    height: 48px;
  }

  &.cart {
    background: #5B3A32;
    display: flex;
    align-items: center;
    gap: 5px;
  }
}

</style>