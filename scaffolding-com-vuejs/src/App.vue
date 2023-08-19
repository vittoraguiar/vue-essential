<script setup>
import { ref } from 'vue';
import Profile from './components/ProfileItem.vue'
import OptionsApi from './components/OptionsApi.vue'

const mostrarProfile = ref(false);
const mostrarOptionsApi = ref(false);
</script>

<template>
  <div>
    <h1>Composition API x Options API</h1>
    <p>Aprendendo as diferenças entre Composition API e Options API, além de conceitos como as diretivas e templates do Vue.js.</p>
    <input type="checkbox" v-model="mostrarProfile" style="margin-right: 10px;">Mostrar Composition API
    <input type="checkbox" v-model="mostrarOptionsApi">Mostrar Options API
  </div>
  <Profile v-if="mostrarProfile" />
  <OptionsApi v-if="mostrarOptionsApi" />
</template>

<style></style>