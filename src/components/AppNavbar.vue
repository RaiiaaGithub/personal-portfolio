<template>
    <nav class="container-xl">
        <ul class="links">
            <li id="logo"><a href="#home">R</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#contact">Contacts</a></li>
        </ul>

        <ul class="social-media">
            <li><a href="https://github.com/RaiiaaGithub" target="_blank">Github</a></li>
            <li><a href="https://www.linkedin.com/in/r%C3%BAben-alves-20232a261/" target="_blank">LinkedIn</a></li>
            <li><a href="https://www.instagram.com/ruben.alves02/" target="_blank">Instagram</a></li>
        </ul>
    </nav>
</template>

<script setup lang="ts">

</script>

<style scoped>
nav {
    position: fixed;
    z-index: 100;
    inset: 0 0 auto 0;
    padding: 1rem;

    display: flex;
    justify-content: space-between;
    align-items: baseline;
}

ul {
    display: flex;
    gap: 1rem;
    list-style-type: none;
    color: white;

    align-items: baseline;
}

ul li a {
    text-decoration: none;
    color: white;
    text-transform: uppercase;
    transition: all 150ms ease-in;
    position: relative;
    padding: 1rem 1rem .5rem 1rem;
}

li a:hover {
    color: var(--color-accent);
}

.links li:not(#logo) a::after {
    content: "";
    position: absolute;
    width: 100%;
    height: 2px;
    background-image: linear-gradient(90deg, transparent 0%, var(--color-accent) 50%, transparent 100%);

    bottom: 0;
    left: 0;

    transform: scaleX(0);
    transition: transform 300ms ease-in-out;
}

.links li:not(#logo) a:hover::after {
    transform: scaleX(1);
}

.links #logo {
    flex-basis: 5rem;
}

.links #logo a {
    padding: 0;
    font-size: 3rem;
    font-weight: 700;
    font-family: 'Damion', cursive;
}
</style>