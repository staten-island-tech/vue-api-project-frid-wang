<template>
  <div class="main-container">
    <div class="exchange"></div>
    <div class="reset">
      <button class="reset-button">Reset</button>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.main-container {
  width: 100vw;
  height: 80vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.exchange {
  width: 65vw;
  height: 50vh;
  box-shadow: 25px 20px 2.5rem #3f3f3f;
  border-bottom-left-radius: 12.5vh;
  border-top-right-radius: 12.5vh;
  margin: 2.5vh;
}
.reset {
  width: 10vw;
  height: 5vh;
}
.reset-button {
  width: 10vw;
  height: 5vh;
  box-shadow: 2.5px 2px 0.25rem #3f3f3f;
  border-top-left-radius: 2.5vh;
  border-bottom-right-radius: 2.5vh;
  margin: 2.5vh;
  border: none;
  font-size: 1.25rem;
}
</style>
