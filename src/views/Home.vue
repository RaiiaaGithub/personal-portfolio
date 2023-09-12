<template>
    <div @mousemove="animateHero" class="hero" id="home">
        <HomeHeroContent ref="heroContent" />
        <HomeHero ref="heroSection" />
    </div>
</template>

<script setup lang="ts">
import HomeHeroContent from '../components/HomeHeroContent.vue';
import HomeHero from '../components/HomeHero.vue';
import { onMounted, ref } from 'vue';

const heroContent = ref<InstanceType<typeof HomeHeroContent> | null>(null)
const heroSection = ref<InstanceType<typeof HomeHero> | null>(null)

function animateHero(e: Event) {
    if (!heroContent.value) { return; }
    if (!heroSection.value) { return; }
    
    const rect = (e.currentTarget as HTMLElement).getBoundingClientRect();

    const x = (e as MouseEvent).clientX;
    const y = (e as MouseEvent).clientY;

    heroContent.value.textContent?.animate({
        transform: `translate(${x / 100}px, ${y / 100}px)`
    }, {
        duration: 800,
        fill: "forwards"
    });

    heroContent.value.imgContent?.animate({
        transform: `translate(${x / 50}px, ${y / 50}px)`
    }, {
        duration: 800,
        fill: "forwards" 
    })
}
</script>

<style scoped>
body {
    overflow: hidden;
}
div {
    overflow: hidden;
}

</style>