<template>
    <div>
        <nav class="navbar navbar-dark bg-dark">
            <div class="container-fluid">
                <button class="navbar-toggler d-md-none" type="button" @click="toggleSidebar">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <router-link to="/" class="navbar-brand ms-auto">
                    <span class="navbar-title">{{ displayTitle}}</span>
                </router-link>
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <router-link to="/" class="nav-link">Login</router-link>
                    </li>
                </ul>
            </div>
        </nav>
    </div>
</template>

<script setup>
import { inject, ref, onMounted, onUnmounted } from 'vue';

// Texto que muestra las dimensiones  de la ventana
const text = ref(`width: ${window.innerWidth}, height: ${window.innerHeight}`);
// Titulo que deseas mostrar en la barra de navegación
const title = 'Mi Aplicación Vue con Laravel';
const displayTitle = ref(title);

// Función para actualizar las dimensiones de la ventana
const updateWindowDimensiones = () => {
    text.value = `width: ${window.innerWidth}, height: ${window.innerHeight}`;
    if (window.innerWidth <= 768) { // Ajusta este valor segun tus necesidades
        if (title.length > 20) {
            displayTitle.value = `${title.slice(0, 20)}...`;
        } else {
            displayTitle.value = title;
        }
    } else if ((window.innerWidth > 768)) {
        displayTitle.value = title;
    }
};

// Agregar el listener del evento 'resize' cuando el componente se monta
onMounted(() => {
    window.addEventListener('resize', updateWindowDimensiones);
    if (window.innerWidth <= 768) {
        displayTitle.value = `${title.slice(0, 20)}...`;
    } else {
        displayTitle.value = title;
    }
});

// Eliminar el listener del evento 'resize' cuando el componente se desmonta
onUnmounted(() => {
    window.removeEventListener('resize', updateWindowDimensiones);
});

const toggleSidebar = inject('toggleSidebar');
</script>

<style scoped>
.navbar {
    height: 55px;
}
</style>