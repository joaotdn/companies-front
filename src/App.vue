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
      <div class="row">
        <button href="#" class="button" :disabled="currentPage > lastPage" @click="listCompanies">Carregar mais</button>
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
    let companies = ref([]);
    let lastPage = ref();
    let currentPage = ref(1);

    const listCompanies = () => {
      http.get('/companies', {
        params: {
          page: currentPage.value,
          state: null,
          city: null
        }
      })
        .then(res => res.data)
        .then(res => {
          res.data.forEach((obj) => companies.value.push(obj));
          lastPage.value  = res.meta.last_page;
          if (currentPage.value <= lastPage.value) {
            currentPage.value++;
          }
        });
    };

    onMounted(() => {
      listCompanies();
    });

    return {
      companies,
      lastPage,
      currentPage,
      listCompanies
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

  > .row {
    padding: $gutter;
    text-align: center;
    width: 100%;
    button {
      border: none;
      border-radius: 4px;
      margin: 0;
      padding: 1rem 0;
      width: 200px;
      background-color: $success;
      color: $white;
      font-size: 16px;
      font-weight: 700;
      display: inline-block;
      cursor: pointer;
      transition: background-color 0.3s linear;
      &:hover {
        background-color: darken($success, 5%);
      }
      &[disabled] {display: none;}
    }
  }
}
</style>
