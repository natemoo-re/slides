<template>
    <h1 class="flex justify-between items-baseline w-full">
        <code>{{ name }}</code>
        <span class="text-lg">Example</span>
    </h1>

    <p class="flex justify-between items-baseline w-full">
        <span>{{ description }}</span>
        <a :href="url" v-if="url.includes('github.com')"><mdi-github class="text-sm" /> {{ url.replace(/^https?:\/\/github\.com\//, '').replace(/\/$/, '') }}</a>
        <a :href="url" v-else><ph-link-simple-bold class="text-sm" /> {{ url.replace(/^https?:\/\//, '').replace(/\/$/, '') }}</a>
    </p>
</template>

<script setup>
defineProps(['name', 'description', 'url'])
</script>

