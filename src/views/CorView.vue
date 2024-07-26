<script setup>
import { ref, reactive, onMounted } from "vue";
import CoresApi from "@/api/cores";
const coresApi = new CoresApi();

const defaultCor = { id: null, nome: "" };
const cores = ref([]);
const cor = reactive({ ...defaultCor });

onMounted(async () => {
  cores.value = await coresApi.buscarTodasAsCores();
});

function limpar() {
  Object.assign(cor, { ...defaultCor });
}

async function salvar() {
  if (cor.id) {
    await coresApi.atualizarCor(cor);
  } else {
    await coresApi.adicionarCor(cor);
  }
  cores.value = await coresApi.buscarTodasAsCores();
  limpar();
}

function editar(cor_para_editar) {
  Object.assign(cor, cor_para_editar);
}

async function excluir(id) {
  await coresApi.excluirCor(id);
  cores.value = await coresApi.buscarTodasAsCores();
  limpar();
}
</script>

<template>
  <h1>Cor</h1>
  <div class="form">
    <input type="text" v-model="cor.nome" placeholder="Nome" />
    <button @click="salvar" class="botao">Salvar</button>
    <button @click="limpar" class="botao">Limpar</button>
  </div>
  <ul>
    <li v-for="cor in cores" :key="cor.id" class="itens">
      <span @click="editar(cor)">
        |{{ cor.id }}| {{ cor.nome }} 
      </span>
      <button @click="excluir(cor.id)" class="botaoX icon mdi mdi-delete"></button>
    </li>
  </ul>
</template>


<style scoped>
input{
  border: 3px solid #65007c;
  border-radius: 10px;
}
.itens{
  display: flex;
  flex-direction: column;
  align-items: start;
}


.botao{
  background-color: #65007c;
  border: 0px;
  border-radius: 10px;
  font-size: large;
  color: white;
}
.botaoX{
  margin-left: 10px;
  color: red;
  background-color: white;
  font-size: 25px;
  border: 0px;
  cursor: pointer;
}
</style>
