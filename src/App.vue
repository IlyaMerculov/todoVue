<script setup lang="ts">
// import HelloWorld from './components/HelloWorld.vue'
// import TheWelcome from './components/TheWelcome.vue'
  import ToDo from './components/ToDo.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="50" height="50" />
    <div class="header-title">TODO</div>
  </header>

  <main>
    <ToDo />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  width: 100%;
  height: 20%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3em;
}

.logo {
  margin: 0 10px 0 0;
}

.header-title{
  margin: 0 0 0 10px
}

main{
  width: 100%;
  height: 80%;
  display: flex;
  align-items: center;
  justify-content: center;
}

</style>
