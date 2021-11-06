<template>
  <section class="nav-bar">
    <img class="logo" src="../assets/media/x.png" alt="" />
    <router-link class="route" to="/">Current Info</router-link> |
    <router-link class="route" to="/about">Historical Data</router-link>
  </section>
</template>

<script>
export default {};
</script>

<style scoped>
.navbar {
}
.logo {
  height: 10vh;
}
.route {
}
</style>
