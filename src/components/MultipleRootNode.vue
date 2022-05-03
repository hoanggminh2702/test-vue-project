<template>
  <header></header>
  <section :class="myCusClass" @click="handleChangeClassState" v-bind="$attrs">
    Test MultipleRootNode
  </section>
  <footer></footer>
</template>

<script lang="ts">
import { ref } from "vue";

export default {
  inheritAttrs: false,
};
</script>

<script setup lang="ts">
const aClass = ref(false);
const myCusClass = ref({
  cusA: aClass,
  b: false,
});

const handleChangeClassState = () => {
  aClass.value = !aClass.value;
};
</script>
