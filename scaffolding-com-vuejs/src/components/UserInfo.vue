<script setup>
defineProps(['user']);
</script>

<template>
    <div>
        <img :src="user.avatar_url">
        <strong>@{{ user.login }}</strong>
        <h1>{{ user.name }}</h1>
        <h2>{{ user.company }}</h2>
        <span>{{ user.bio }}</span>
    </div>
</template>

<style scoped>
img {
    border: 1px solid #e5e5e5;
    border-radius: 999px;
    display: block;
    margin: 1rem auto;
    width: 8rem;
    height: 8rem;
}

span {
    display: block;
    margin: 1rem auto;
}
</style>