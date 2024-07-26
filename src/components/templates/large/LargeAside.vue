<script setup>
import LogoTitle from '@/components/templates/LogoTitle.vue';
</script>
<template>
  <div class="logo_and_menu">
    <logo-title class="mb-2" />
    <div class="divider" />
    <div class="menu">
      <router-link to="/">
        <i class="icon mdi mdi-home-outline" /> Home
      </router-link>
     <router-link to="/perfil">
        <i class="icon mdi mdi-account-circle" /> Perfil
      </router-link> 
    </div>
    <div class="divider" />
    <div class="menu">
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
      <router-link to="/login">
        <i class="icon mdi mdi-login" /> Login
      </router-link>
    </div>
  </div>
  <logo-title/>
</template>
<style scoped>
.mb-2 {
  margin-bottom: 1.5rem;
}

.icon {
  font-size: 2rem;
  align-self: center;
}
.divider {
  border-top: 1rem solid #65007c;
}
.menu {
  padding: 3rem;
}

.menu a {
  display: flex;
  align-items: center;
  text-decoration: none;
  color: #65007c;
  gap: 1rem;
  font-size: 1.3rem;
  margin-top: 2.2rem;
}
</style>