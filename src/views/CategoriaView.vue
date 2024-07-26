<script setup>
import { ref, reactive, onMounted } from "vue";
import CategoriasApi from "@/api/categorias";
const categoriasApi = new CategoriasApi();

const defaultCategoria = { id: null, descricao: "" };
const categorias = ref([]);
const categoria = reactive({ ...defaultCategoria });

onMounted(async () => {
  categorias.value = await categoriasApi.buscarTodasAsCategorias();
});

function limpar() {
  Object.assign(categoria, { ...defaultCategoria });
}

async function salvar() {
  if (categoria.id) {
    await categoriasApi.atualizarCategoria(categoria);
  } else {
    await categoriasApi.adicionarCategoria(categoria);
  }
  categorias.value = await categoriasApi.buscarTodasAsCategorias();
  limpar();
}

function editar(categoria_para_editar) {
  Object.assign(categoria, categoria_para_editar);
}

async function excluir(id) {
  await categoriasApi.excluirCategoria(id);
  categorias.value = await categoriasApi.buscarTodasAsCategorias();
  limpar();
}
</script>

<template>
  <h1>Categoria</h1>
  <div class="form">
    <input type="text" v-model="categoria.descricao" placeholder="Descrição" />
    <button @click="salvar" class="botao">Salvar</button>
    <button @click="limpar" class="botao">Limpar</button>
  </div>
  <ul>
    <li v-for="categoria in categorias" :key="categoria.id" class="itens">
      <span @click="editar(categoria)">
        |{{ categoria.id }}| {{ categoria.descricao }} 
      </span>
      <button @click="excluir(categoria.id)" class="botaoX icon mdi mdi-delete"></button>
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
