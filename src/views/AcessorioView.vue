<script setup>
import { ref, reactive, onMounted } from "vue";
import AcessoriosApi from "@/api/acessorios";
const acessoriosApi = new AcessoriosApi();

const defaultAcessorio = { id: null, nome: "" };
const acessorios = ref([]);
const acessorio = reactive({ ...defaultAcessorio });

onMounted(async () => {
  acessorios.value = await acessoriosApi.buscarTodasAsAcessorios();
});

function limpar() {
  Object.assign(acessorio, { ...defaultAcessorio });
}

async function salvar() {
  if (acessorio.id) {
    await acessoriosApi.atualizarAcessorio(acessorio);
  } else {
    await acessoriosApi.adicionarAcessorio(acessorio);
  }
  acessorios.value = await acessoriosApi.buscarTodasAsAcessorios();
  limpar();
}

function editar(acessorio_para_editar) {
  Object.assign(acessorio, acessorio_para_editar);
}

async function excluir(id) {
  await acessoriosApi.excluirAcessorio(id);
  acessorios.value = await acessoriosApi.buscarTodasAsAcessorios();
  limpar();
}
</script>

<template>
  <h1>Acessorio</h1>
  <div class="form">
    <input type="text" v-model="acessorio.descricao" placeholder="Descrição" />
    <button @click="salvar" class="botao">Salvar</button>
    <button @click="limpar" class="botao">Limpar</button>
  </div>
  <ul>
    <li v-for="acessorio in acessorios" :key="acessorio.id" class="itens">
      <span @click="editar(acessorio)">
        |{{ acessorio.id }}|  {{ acessorio.descricao }} 
      </span>
      <button @click="excluir(nome.id)" class="botaoX icon mdi mdi-delete"></button>
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
