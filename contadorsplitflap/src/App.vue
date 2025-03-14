<script setup>
import { ref, onMounted } from 'vue';
import SplitFlapDisplay from './components/SplitFlapDisplay.vue';
import axios from 'axios';

const followerCount = ref(0);
const accessToken = "IGAANTJNYPFOJBZAE1ORkxwNDNoM245T2JTd2Rnb25GRzNTeEdfU2g4cE9vbmVtOGRPQzhxSHFlaEctR0FBcVplNTlkSTJSZAUlPNUFMdmVYQ09CY2hYdGp0ODA4VWlqdmhUbnNMVTROYlp1RlRhMlQ4VHc3Ujg0RndCVFhVTTRiYwZDZD";
const apiURL = `https://graph.instagram.com/me?fields=followers_count&access_token=${accessToken}`;

async function fetchFollowers() {
  try {
    const response = await axios.get(apiURL);
    if (response.data && response.data.followers_count) {
      followerCount.value = response.data.followers_count;
    }
  } catch (error) {
    console.error("Erro ao buscar os seguidores:", error);
  }
}

onMounted(() => {
  fetchFollowers();
  setInterval(fetchFollowers, 5000);
});
</script>

<template>
  <div>
    <h1>Contador de Seguidores</h1>
    <SplitFlapDisplay :number="followerCount" />
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  font-size: 2rem;
  color: #333;
  margin-bottom: 20px;
}
</style>