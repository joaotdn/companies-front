<template>
  <div class="companies-app">
    <top-bar />
    <div class="container"></div> 
  </div>
</template>

<script>
import TopBar from './components/TopBar.vue';

export default {
  name: 'companiesApp',
  components: {
    TopBar
  }
}
</script>

<style scoped lang="scss">
@import './assets/scss/variables';
.container {
  width: 100%;
  max-width: 740px;
  margin: 0 auto;
  background-color: $white;
  border-radius: 8px;
  padding: calc($gutter *2) $gutter;
}
</style>
