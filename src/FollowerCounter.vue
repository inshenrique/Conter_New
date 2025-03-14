<script setup lang="ts">
import { ref, onMounted } from "vue";

// Token de acesso do Instagram (⚠️ Substitua pelo seu token seguro)
const token = "IGAANTJNYPFOJBZAE1ORkxwNDNoM245T2JTd2Rnb25GRzNTeEdfU2g4cE9vbmVtOGRPQzhxSHFlaEctR0FBcVplNTlkSTJSZAUlPNUFMdmVYQ09CY2hYdGp0ODA4VWlqdmhUbnNMVTROYlp1RlRhMlQ4VHc3Ujg0RndCVFhVTTRiYwZDZD";
const followers = ref(0);

const fetchFollowers = async () => {
  try {
    const response = await fetch(`https://graph.instagram.com/me?fields=username,followers_count&access_token=${token}`);
    const data = await response.json();
    followers.value = data.followers_count;
  } catch (error) {
    console.error("Erro ao buscar seguidores:", error);
  }
};

onMounted(fetchFollowers);
</script>

<template>
  <div class="counter">
    <h1>{{ followers }}</h1>
  </div>
</template>

<style scoped>
.counter {
  font-size: 3rem;
  font-weight: bold;
  text-align: center;
}
</style>
