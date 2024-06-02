<template>
  <button class="primary-button">
    <component class="primary-button__icon" v-if="icon" :is="icon"></component>
  </button>
</template>

<script setup>
defineProps( {
  icon: {
    type: Object,
    default: null
  }
  })
</script>

<style lang="scss" scoped>

.primary-button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 10px 12px;
  cursor: pointer;
  transition: border-color 0.25s;
  background-color: #333333;

  &__icon {
    width: 25px;
    height: 25px;
  }
    &:hover :deep(.primary-button__icon path) {
      fill: white;
      transition: fill .25s ease-out;
    }
    &:active :deep(.primary-button__icon path) {
      fill: black;
      transition: fill .25s ease-out;
    }
  }
</style>