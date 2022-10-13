<template>
    <div class="form-control">
        <label :for="id">Buscar</label>
        <input type="search" :name="id" :id="id" placeholder="Digite o nome" :value="name"
            @input="$emit('update:name', $event.target.value)">
        <button type="button" @click="$emit('searchCompany')" :disabled="!name">
            <img :src="searchIcon" alt="Ícone de busca">
        </button>
    </div>
</template>

<script setup>
import searchIcon from '../assets/search.png'
defineProps(['name', 'id']);
defineEmits(['update:name', 'searchCompany']);
</script>
<style scoped lang="scss">
@import '../assets/scss/components/form-controls';
</style>