<template>
    <section class="hero" @mousemove="heroEffects" ref="heroSection">
        <div class="animated-grid" ref="animatedGrid">
            <div class="cell" v-for="index in 3000"></div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";

const heroSection = ref<HTMLDivElement | null>(null);
const animatedGrid = ref<HTMLDivElement | null>(null);
defineExpose({heroSection, animatedGrid});

function heroEffects(e: Event) {
    const rect = (e.currentTarget as HTMLElement).getBoundingClientRect()

    const x = (e as MouseEvent).clientX;
    const y = (e as MouseEvent).clientY;

    heroSection.value?.animate({
        top: `${y - rect.top / 2}px`
    }, {
        duration: 800,
        fill: "forwards",
        pseudoElement: "::before"
    })

    animatedGrid.value?.animate({
        top: `${y - rect.top / 2}px`,
        left: `${x - rect.left / 2}px`
    }, {
        duration: 800,
        fill: "forwards",
        pseudoElement: "::before"
    })
}

</script>

<style scoped>
.hero {
    width: 100%;
    height: 100vh;

    background-color: var(--color-base);
    position: relative;
    overflow: hidden;
}

.hero::before {
    content: "";
    position: absolute;

    width: 2px;
    height: 100px;
    background-image: linear-gradient(0deg, transparent 0%, var(--color-accent) 50%, transparent 100%);

    top: var(--mouse-y, 0);
    left: 0;
    transform: translateY(-50%);

    z-index: 10;
}

.animated-grid {
    width: 100%;
    background-color: var(--color-base);
    background-blend-mode: overlay;
    background-image: linear-gradient(325deg, var(--color-accent-darker), var(--color-primary-darker) 50%, var(--color-accent-darker) 100%);
    position: absolute;

    display: grid;
    grid-auto-flow: row;
    grid-template-columns: repeat(6, 1fr);
    gap: 1px;
    pointer-events: none;
}

.animated-grid::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    transform: translate(-50%, -50%);

    width: 1000px;
    aspect-ratio: 1/1;
    background-image: radial-gradient(circle, var(--color-primary-lighter) 0%, transparent 50%);
    opacity: .5;
}

.cell {
    overflow: hidden;
    background-color: var(--color-base);
    aspect-ratio: 1/1;
    z-index: 1;

    animation: move 30s infinite;
}
</style>