<template>
  <div class="companies-app">
    <top-bar />
    <div class="container">
      <div v-for="company in companies" :key="company.id" class="col">
        <card
          :title="company.name"
          :description="company.description"
          :email="company.email"
        />
      </div>
    </div> 
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import http from './http';
import TopBar from './components/TopBar.vue';
import Card from './components/Card.vue';

export default {
  name: 'companiesApp',
  components: {
    TopBar,
    Card
  },
  setup() {
    let companies = ref();

    onMounted(() => {
      http.get('/companies')
        .then(res => res.data)
        .then(res => companies.value = res.data);
    });

    return {
      companies
    }
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
  padding: $gutter;
  display: flex;
  flex-wrap: wrap;
  > .col {
    width: 100%;
    padding: $gutter;

    @media screen and (min-width: 741px) {
      width: 50%;
      float: left;
    }
  }
}
</style>
