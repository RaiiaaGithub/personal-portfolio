<template>
    <main>
        <HomeHeroTitle ref="heroTitle"/>
        <HomeHero ref="heroSection" />
    </main>
</template>

<script setup lang="ts">
import HomeHeroTitle from '../components/HomeHeroTitle.vue';
import HomeHero from '../components/HomeHero.vue';
import { onMounted, ref } from 'vue';

const heroTitle = ref()
const heroSection = ref()

onMounted(() => {
    console.log(heroTitle.value)
    console.log(heroSection.value)
})
</script>

<style scoped>

</style>