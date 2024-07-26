<script setup>
import { ref, reactive, onMounted } from "vue";
import MarcasApi from "@/api/marcas";
const marcasApi = new MarcasApi();

const defaultMarca = { id: null, nome: "", nacionalidade: "" };
const marcas = ref([]);
const marca = reactive({ ...defaultMarca });

onMounted(async () => {
  marcas.value = await marcasApi.buscarTodasAsMarcas();
});

function limpar() {
  Object.assign(marca, { ...defaultMarca });
}

async function salvar() {
  if (marca.id) {
    await marcasApi.atualizarMarca(marca);
  } else {
    await marcasApi.adicionarMarca(marca);
  }
  marcas.value = await marcasApi.buscarTodasAsMarcas();
  limpar();
}

function editar(marca_para_editar) {
  Object.assign(marca, marca_para_editar);
}

async function excluir(id) {
  await marcasApi.excluirMarca(id);
  marcas.value = await marcasApi.buscarTodasAsMarcas();
  limpar();
}
</script>

<template>
  <h1>Marca</h1>
  <div class="form">
    <input type="text" v-model="marca.nome" placeholder="nome" /> 
    <input type="text" v-model="marca.nacionalidade" placeholder="Nacionalidade" /> 
    <button @click="salvar" class="botao">Salvar</button> 
    <button @click="limpar" class="botao">Limpar</button>
  </div>
  <ul>
    <li v-for="marca in marcas" :key="marca.id" class="itens">
      <span @click="editar(marca)" class="nomes">
        |{{ marca.id }}| {{ marca.nome }} - {{ marca.nacionalidade }}
      </span>
      <button @click="excluir(marca.id)" class="botaoX icon mdi mdi-delete"></button>
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

.nomes{
  font-size: large;
}
</style>
