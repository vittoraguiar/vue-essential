<script setup>
import { ref } from 'vue';

const emit = defineEmits(['username']);

const username = ref('');

const handleSubmit = (ev) => {
    ev.preventDefault();
    emit('username', username.value);
};
</script>

<template>
    <div>
        <form @submit="handleSubmit">
            <div class="inputAndButton">
                <input type="text" v-model.lazy="username">
                <button>Pesquisar Usuário</button>
            </div>
        </form>
    </div>
</template>