<template>
  <div class="btn-wrapper">
    <button class="btn" v-bind="$attrs">This is Button</button>
  </div>
</template>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<script setup lang="ts"></script>
