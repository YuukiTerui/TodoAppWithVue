<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg"/>
    <div class="wrapper">

      <h1>TodoAppWithVue</h1>
    </div>
  </header>

  <main>
  </main>
</template>


<script setup lang="ts">

</script>


<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
  width: 64px;
  height: 64px;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
