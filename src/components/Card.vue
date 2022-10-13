<template>
    <div class="card">
        <h2 class="card__title">{{ title }}</h2>
        <p class="card_description">{{ description }}</p>
        <div class="card__links">
            <a :href="`mailto:${email}`">Enviar email</a>
            <a href="#">Whatsapp</a>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        title: {
            type: String,
            default: null
        },
        description: {
            type: String,
            default: null
        },
        email: {
            type: String,
            default: null
        },
        whatsapp: {
            type: String,
            default: null
        }
    }
}
</script>

<style scoped lang="scss">
@import '../assets/scss/components/card';
</style>