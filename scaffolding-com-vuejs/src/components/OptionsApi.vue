<script>
export default {
    data() {
        return {
            name: '',
            login: '',
            bio: '',
            company: '',
            avatar_url: '',
            searchInput: '',
            repos: []
        }
    },
    methods: {
        async fetchGithubUser() {
            if (this.searchInput === '') {
                return alert('Digite um usuário do GitHub');
            }
            const res = await fetch(`https://api.github.com/users/${this.searchInput}`);
            const data = await res.json();
            this.name = data.name;
            this.login = data.login;
            this.bio = data.bio;
            this.company = data.company;
            this.avatar_url = data.avatar_url;

            this.fetchUserRepositories(this.login);
        },

        fetchUserRepositories(username) {
            const res = fetch(`https://api.github.com/users/${username}/repos`);
            const data = res.json();
            this.repos = data;
        }
    }
}
</script>

<template>
    <div>
        <h2 style="margin-top: 30px;">Options API</h2>
        <div class="inputAndButton">
            <input type="text" v-model="searchInput" @keyup.enter="fetchGithubUser">
            <button @click="fetchGithubUser">Pesquisar Usuário</button>
        </div>
        <div v-if="login !== ''">
            <img v-bind:src="avatar_url">
            <strong>@{{ login }}</strong>
            <h1>{{ name }}</h1>
            <h2>{{ company }}</h2>
            <span>{{ bio }}</span>
        </div>
    </div>
    <section v-if="repos.length > 0">
        <article v-for="repo in repos" :key="repo.id">
            <h3>{{ repo.name }}</h3>
            <p>{{ repo.description }}</p>
            <a :href="repo.html_url" target="_blank">Ver no GitHub</a>
        </article>
    </section>
</template>