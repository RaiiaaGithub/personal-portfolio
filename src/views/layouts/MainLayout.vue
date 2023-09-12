<template>
    <AppNavbar />

    <main>
        <slot />
    </main>

    <AppFooter />
</template>

<script setup lang="ts">
import AppNavbar from '../../components/AppNavbar.vue'
import AppFooter from '../../components/AppFooter.vue'
</script>

<style scoped>

</style>