<template>
  <button class="control-button">
    <slot />
  </button>
</template>

<style scoped>
.control-button {
  background-color: transparent;
  border: none;
  cursor: pointer;
  outline: none;
  padding: 0;
}
</style>