<script setup>
import { reactive, computed, onMounted } from 'vue';
import UserInfo from './UserInfo.vue';
import UserRepositories from './UserRepositories.vue';
import UserForm from './UserForm.vue';

const user = reactive({
    name: '',
    login: '',
    bio: '',
    company: '',
    repos: [],
    avatar_url: ''
});

const fetchGithubUser = async (username) => {
    if (username === '') {
        return alert('Digite um usuário do GitHub');
    }
    const res = await fetch(`https://api.github.com/users/${username}`);
    const data = await res.json();
    user.name = data.name;
    user.login = data.login;
    user.bio = data.bio;
    user.company = data.company;
    user.avatar_url = data.avatar_url;

    await fetchUserRepositories(user.login);
};

const fetchUserRepositories = async (username) => {
    const res = await fetch(`https://api.github.com/users/${username}/repos`);
    const data = await res.json();
    user.repos = data;
};

const reposCountMessage = computed(() =>
    user.repos.length > 0
        ? `${user.name} possui ${user.repos.length} repositórios públicos`
        : `${user.name} não possui repositórios públicos`
);

onMounted(() => {
    console.log('Abriu CompositionApi.vue');
});
</script>

<template>
    <h1 style="margin-top: 30px;">Composition API</h1>

    <UserForm @username="fetchGithubUser" />

    <UserInfo v-if="user.login !== ''" :user="user" />

    <section v-if="user.repos.length > 0">
        <h2>{{ reposCountMessage }}</h2>
        <UserRepositories :repositories="user.repos" />
    </section>
</template>