<template>
    <div :class="['sidebar', { active: isActive }]">
        <div class="row">
            <div class="dropdown mt-6 col-8 company-logo">
                <a href="#" class="d-flex align-items-center mb-md-0 me-md-auto text-white text-decoration-none">
                    <i class="fab fa-vuejs me-2" style="font-size: 40px;"></i>
                    <span class="fs-4">Sidebar</span>
                </a>
            </div>
            <div class="col-3">
                <button @click="toggleSidebar" class="btn btn-sm btn-dark mt-6 toggleDark" aria-label="Toggle sidebar">
                    <i class="fas fa-chevron-left"></i> <!-- Icono de flecha a la Izquierda-->
                </button>
            </div>
        </div>
        <hr>
        <ul class="nav nav-pills flex-column mb-auto">
            <li>
                <router-link to="/dashboard" class="nav-link">
                    <i class="fas fa-tachometer-alt me-2"></i>
                    Dashboard
                </router-link>
            </li>
            <li>
                <router-link to="/customers" class="nav-link">
                    <i class="fas fa-users me-2"></i>
                    Customers
                </router-link>
            </li>
            <li class="mb-1">
                <button class="btn btn-toggle align-items-center rounded collapsed nav-link" data-bs-toggle="collapse"
                    data-bs-target="#home-collapse" aria-expanded="false">
                    Users & Roles
                </button>
                <div class="collapse" id="home-collapse" style="">
                    <ul class="nav flex-column ms-3 text-extra-small">
                        <li>
                            <router-link to="/users" class="nav-link">
                                <i class="fas fa-user me-2"></i>
                                Users
                            </router-link>
                        </li>
                        <li>
                            <router-link to="/roles" class="nav-link">
                                <i class="fas fa-user-shield me-2"></i>
                                Roles
                            </router-link>
                        </li>
                        <li>
                            <router-link to="/permissions" class="nav-link">
                                <i class="fas fa-lock me-2"></i>
                                Permissions
                            </router-link>
                        </li>
                    </ul>
                </div>
            </li>
        </ul>
        <hr>
        <div class="dropdown mt-6 user-profile">
            <a href="#" class="d-flex align-items-center nav-link text-decoration-none dropdown-toggle"
                id="dropdownUser1" data-bs-toggle="dropdown" aria-expanded="false">
                <div class="avatar bg-primary text-white rouded-circle d-flex align-items-center justify-content-center me-2"
                    style="width: 32px; height: 32px;">
                    <span class="text-uppercase">J F</span>
                </div>
                <div class="d-flex flex-column">
                    <strong>Jose Fermin</strong>
                    <small>Joseasaelf@gmail.com</small>
                </div>
            </a>
            <ul class="dropdown-menu dropdown-menu-dark text-small shadow" aria-labelledby="dropdownUser1">
                <li><a class="dropdown-item" href="#">Settings</a></li>
                <li><a class="dropdown-item" href="#">Profile</a></li>
                <li>
                    <hr class="dropdown-divider">
                </li>
                <li><a class="dropdown-item" href="#" @click="logout">Sign out</a></li>
            </ul>
        </div>
    </div>
</template>

<script setup>
import { inject } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
// Funcion para el toggle del sidebar en el boton de navbar
const isActive = inject('isActive')
const toggleSidebar = inject('toggleSidebar')
</script>

<style scoped>
.sidebar {
    width: 250px;
    position: fixed;
    top: 0;
    left: 0;
    height: 100%;
    background-color: #343a40;
    padding-top: 1rem;
    z-index: 1000;
    transition: transform 0.3s ease;
    display: flex;
    flex-direction: column;
    overflow-y: auto;
    overflow-x: hidden;
}

.sidebar .nav-link {
    color: #fff;
    transition: color 0.3;
    display: flex;
    align-items: center;
}

.sidebar .nav-link:hover {
    color: green;
    text-decoration: none;
}

.sidebar .nav-link i {
    width: 20px;
    padding-right: 10px;
}

.toggleDark {
    display: none;
}

@media (max-width: 768px) {
    .sidebar {
        transform: translateX(-250%);
    }

    .content {
        margin-left: 0;
        padding-right: 20px;
    }

    .sidebar.active {
        transform: translateX(0);
    }

    .content.active {
        margin-left: 250px;
    }

    #sidebarToggle {
        display: block;
    }

    .toggleDark {
        display: block;
    }
}

#sidebarToggle {
    display: none;
    position: fixed;
    top: 1rem;
    left: 1rem;
    z-index: 1100;
    background-color: #343a40;
    color: #fff;
    border: none;
    padding: 0.5rem 1rem;
    cursor: pointer;
}

.sidebar hr {
    border-color: #fff;
}

.user-profile {
    margin-bottom: 30px;
    margin-left: 20px;
}

.company-logo {
    margin-left: 20px;
}

.text-extra-small {
    font-size: 0.80rem;
}

.btn-toggle::before {
    content: '\f078';
    /* Unicode para la flecha hacia abajo (FontAwesome) */
    font-family: 'FontAwesome';
    display: inline-block;
    margin-right: 20px;
    transition: transform 0.3s ease;
}

.btn-toggle.collapsed::before {
    content: '\f054';
    /* Unicode para la flecha hacia la derecha (FontAwesome) */
    transform: rotate(0);
}

.btn-toggle[aria-expanded="true"]::before {
    transform: rotate(0deg);
}

.btn-toggle.collapsed[aria-expanded="true"]::before {
    content: '\f078';
    /* Asegura que la flecha hacia abajo se mantenga */
    transform: rotate(0);
}
</style>