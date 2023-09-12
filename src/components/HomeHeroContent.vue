<template>
    <div class="hero-content" ref="heroContent">
        <div class="text-content" ref="textContent">
            <p class="intro">Hello, my name is...</p>
            <h1>{{ title ?? "Rúben Alves" }}<br></h1>
            <h2>I'm a <span ref="spanRef" id="rewrite">{{ wordArray[counter] }}</span> developer.</h2>
        </div>
        <div class="image-content" ref="imgContent">
            <img src="../assets/images/edit-portfolio.png" alt="" srcset="">
        </div>
    </div>
</template>
  
<script setup lang="ts">
import { onMounted, ref } from 'vue';

const { title, words } = defineProps<{ title?: string, words?: string[] }>();

const spanRef = ref<HTMLSpanElement | null>(null);
const heroContent = ref<HTMLDivElement | null>(null);
const textContent = ref<HTMLDivElement | null>(null);
const imgContent = ref<HTMLDivElement | null>(null);
defineExpose({heroContent, textContent, imgContent})

onMounted(() => {
    setInterval(handleSpanText, 5000)
})

const wordArray = words ?? ["frontend", "backend", "fullstack"];
let counter = 0;

async function handleSpanText() {

    if (!spanRef.value) { return; }

    if (counter === wordArray.length - 1) {
        counter = 0;
    } else {
        counter++;
    }

    const nextWord = wordArray[counter];

    if (await removeCharacter()) {
        writeWord(nextWord);
    }
}

async function removeCharacter() {
    return await new Promise((resolve) => {
        const removeCharsTimer = setInterval(() => {
            if (!spanRef.value) { return; }

            spanRef.value.textContent = spanRef.value.textContent?.slice(0, -1) ?? "";

            if (spanRef.value.textContent === "") {
                setTimeout(() => {
                    resolve(true)
                }, 500)
                clearInterval(removeCharsTimer);
            }
        }, 100);
    })
}

async function writeWord(word: string) {
    return await new Promise(resolve => {
        const addCharsTimer = setInterval(() => {
            if (!spanRef.value) { return; }

            spanRef.value.textContent += word.charAt(spanRef.value?.textContent?.length ?? 0);

            if (spanRef.value.textContent === word) {
                clearInterval(addCharsTimer);
                resolve(true)
            }
        }, 100);
    })
}

</script>
  
<style scoped>
.hero-content {
    position: absolute;
    z-index: 5;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    gap: 7rem;

    pointer-events: none;
}

p {
    color: white;
    font-size: 1.3rem;
    font-weight: 100;
}

h1 {
    color: var(--color-accent);
    font-size: 6rem;
}

h2 {
    font-weight: 400;
    color: white;
    text-align: right;
    font-size: 2em;
}

#rewrite {
    position: relative;
    transition: all 150ms ease-in-out;
    font-weight: 700;
    color: var(--color-accent);
    text-transform: uppercase;
}

#rewrite::after {
    content: "";
    position: absolute;
    right: -2px;
    top: 0;
    width: 2px;
    height: 100%;
    background-color: var(--color-accent);
    animation: blink 500ms ease-out infinite;
}

.image-content {
    width: 600px;
    height: 500px;
}

img {
    max-width: 100%;
    object-fit: cover;
}

@keyframes blink {
    from,
    to {
        opacity: 1;
    }

    50% {
        opacity: 0;
    }
}
</style>