<template>
  <div class="nav-bar">
    <section class="logo"></section>
    <section class="history" v-if="(x = true)"></section>
    <section class="current" v-if="(x = false)"></section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      x: true,
    };
  },
};
</script>

<style scoped>
</style>