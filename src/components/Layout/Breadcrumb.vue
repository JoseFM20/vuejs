<template>
    <nav aria-label="breadcrumb">
        <ol class="breadcrumb">
            <router-link class="breadcrumb-item" to="/home">Inicio</router-link>
            <li class="breadcrumb-item active" aria-current="page" v-for="item in items" :key="item.path">
                {{ item.name }}
            </li>
        </ol>
    </nav>
</template>

<script setup>
import { useRoute } from 'vue-router';
import { computed } from 'vue';
const route = useRoute();
const items = computed(() => {
    return route.matched
})
</script>

<style scoped>
nav {
    margin-top: 15px;
}
</style>