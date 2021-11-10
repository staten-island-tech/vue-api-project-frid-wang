<template>
  <section id="nav-bar">
     <router-link class="route" to="/"> <img class="logo" src="../assets/media/logo.png" alt="" /></router-link> 
    <div class="sub-nav">
      <router-link class="route" to="/">Current Info</router-link> 
      <router-link class="route" to="/Historical">Historical Data</router-link>
    </div>
   
  </section>
</template>

<script>
export default {};
</script>

<style scoped>
#nav-bar {
  display: flex;
  flex-direction: row;
  width: 80vw;
  justify-content: space-between;
  align-items: center;
  transform: translateX(10%);
}

.sub-nav{
  width: 20%;
  display: flex;
  justify-content: space-evenly;
  transform: translateX(-5%);
}


</style>
