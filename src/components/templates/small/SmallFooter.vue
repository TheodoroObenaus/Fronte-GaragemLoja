<script setup>
import { ref } from 'vue';
import { onBeforeRouteUpdate } from 'vue-router';

const showMenu = ref(false);

onBeforeRouteUpdate(() => {
  showMenu.value = false;
});
</script>
<template>
  <div id="footerMenu" :style="{ display: showMenu ? 'block' : 'none' }">
    <RouterLink to="/">
      <i class="mdi mdi-home-outline" />
      Home
    </RouterLink>
    <router-link to="/marcas">
        <i class="icon mdi mdi-car-lifted-pickup"/> Marca
      </router-link>
      <router-link to="/categorias">
        <i class="icon mdi mdi-car-sports"/> Categoria
      </router-link>
      <router-link to="/Cores">
        <i class="icon mdi mdi-palette"/> Cor
      </router-link>
      <router-link to="/acessorios">
        <i class="icon mdi mdi-engine"/> Acessorios
      </router-link>
  </div>
  <div class="icons">
    <RouterLink to="/">
      <i class="mdi mdi-home-outline" />
      Home
    </RouterLink>
    <RouterLink to="/login">
      <i class="mdi mdi-account" />
      Login
    </RouterLink>

    <div class="hamburger" @click="showMenu = !showMenu">
      <i class="mdi mdi-menu" />
      Menu
    </div>
  </div>
</template>
<style scoped>
#footerMenu {
    position: fixed;
    bottom: 15%;
    right: 0;

    width: 30%;
    border-top: #EEEEEE 1px solid;
    background-color: white;

    display: block;
    padding: 1rem;
}

#footerMenu a {
    display: flex;
    width: 100%;
    justify-content: space-between;
    text-decoration: none;
    color: #65007c;
    font-size: 1rem;
    transition: color 0.3s;
}


.icons {
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: space-between;
    color: #65007c;
}

.icons a,
.icons .hamburger {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-decoration: none;
    color: #65007c;
    font-size: 1rem;
    transition: color 0.3s;
}

.hamburger:hover {
    cursor: pointer;
}
</style>