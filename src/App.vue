<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import SplitFlap from "./components/SplitFlap.vue";

const token = "IGAANTJNYPFOJBZAE1ORkxwNDNoM245T2JTd2Rnb25GRzNTeEdfU2g4cE9vbmVtOGRPQzhxSHFlaEctR0FBcVplNTlkSTJSZAUlPNUFMdmVYQ09CY2hYdGp0ODA4VWlqdmhUbnNMVTROYlp1RlRhMlQ4VHc3Ujg0RndCVFhVTTRiYwZDZD";

const followers = ref("000000"); // Inicializa com zeros
let intervalId: number | undefined; // Armazena o ID do intervalo

const fetchFollowers = async () => {
  try {
    const response = await fetch(`https://graph.instagram.com/me?fields=username,followers_count&access_token=${token}`);
    const data = await response.json();
    followers.value = String(data.followers_count).padStart(6, "0"); // Formata para 6 dígitos
  } catch (error) {
    console.error("Erro ao buscar seguidores:", error);
  }
};

onMounted(() => {
  fetchFollowers(); // Busca os seguidores ao carregar
  intervalId = setInterval(fetchFollowers, 5000); // Atualiza a cada 5s
});

onUnmounted(() => {
  if (intervalId) clearInterval(intervalId); // Remove o intervalo ao sair do componente
});
</script>

<template>
  <pre>
    <SplitFlap v-for="(c, i) in followers" :key="i" :char="c" :duration="5000" />
  </pre>
</template>

<style scoped lang="css">
pre {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 1.5rem;
  height: 100%;
  width: fit-content;
  margin: 0;
  padding: 0;
}
</style>
