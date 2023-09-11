<template>
  HELLO <span ref="spanRef" id="rewrite">{{words[counter]}}</span>
</template>

<script setup lang="ts">
import { onMounted, ref, resolveComponent } from 'vue';

const words = ["WORLD", "MOM", "DAD", "FAMILY"];
let counter = 0;

const spanRef = ref<HTMLSpanElement>();

onMounted(() => {
    setInterval(handleSpanText, 5000)
})

function handleSpanText() {
    
    if (!spanRef.value) { return; }
    if (!spanRef.value.textContent) { return; }
    
    if (counter === words.length - 1) {
        counter = 0;
    } else {
        counter++;
    }

    const nextWord = words[counter];
    changeCharacters(nextWord);
}

async function changeCharacters(word: string) {
    if (!spanRef.value) { return; }

    if (await removeCharacter()) {
        writeWord(word);
    }
}

async function removeCharacter() {
    return await new Promise((resolve) => {
        const removeCharsTimer = setInterval(() => {
            if (!spanRef.value) { return; }

            spanRef.value.textContent = spanRef.value.textContent?.slice(0, -1) ?? "";

            if (spanRef.value.textContent === "") {
                resolve(true)
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
        },100);
    })
}

</script>

<style scoped>

#rewrite {
    position: relative;
    transition: all 150ms ease-in-out;
}

#rewrite::after {
    content: "";
    position: absolute;
    right: -2px;
    top: 0;
    width: 2px;
    height: 100%;
    background-color: blue;
    animation: blink 500ms infinite;
}

@keyframes blink {
    from, to {
        opacity: 1;
    }

    50% {
        opacity: 0;
    }
}

</style>