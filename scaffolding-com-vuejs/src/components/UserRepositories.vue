<script setup>
defineProps(['repositories']);
</script>

<template>
    <div>
        <article v-for="repo in repositories" :key="repo.id">
            <h3>{{ repo.name }}</h3>
            <p>{{ repo.description }}</p>
            <a :href="repo.html_url" target="_blank">Ver no GitHub</a>
        </article>
    </div>
</template>