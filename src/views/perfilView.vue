<script setup>
import { onMounted } from 'vue';
import { PassageUser } from '@passageidentity/passage-elements/passage-user';
import { useAuthStore } from '@/stores/auth';

const authStore = useAuthStore();

const getUserInfo = async () => {
  try {
    const authToken = localStorage.getItem('psg_auth_token');
    const passageUser = new PassageUser(authToken);
    const user = await passageUser.userInfo(authToken);
    if (user) {
      await authStore.setToken(authToken);
    } else {
      authStore.unsetToken();
    }
  } catch (error) {
    authStore.unsetToken();
  }
};

onMounted(() => {
  getUserInfo();
});
</script>

<template>
  <div class="logout">
    <h1>Perfil</h1>
    <div v-if="authStore.loggedIn" class="email">
      {{ authStore.user.email }} 
    </div>
    <router-link  to="/logout">Sair</router-link> 
  </div>
</template>

<style scoped>
.logout {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: larger;
}

.email {
  border-top: 2px solid #65007c;
}
</style>