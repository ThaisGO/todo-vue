<script setup>
import { reactive } from 'vue';

import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  novaTarefa: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false
    },
    {
      titulo: 'Ir para academia',
      finalizada: true
    },
  ]
});

function cadastraTarefa() {
  const tempTarefa = {
    titulo: estado.novaTarefa,
    finalizada: false
  }
  estado.tarefas.push(tempTarefa)
}

// const getTarefasPendentes = () => {
  //   return estado.tarefas.filter(item => !item.finalizada )
  // }
  
  function getTarefasPendentes() {
    return estado.tarefas.filter(item => !item.finalizada).length
  }

  function getFiltroPendentes() {
    return estado.tarefas.filter(item => !item.finalizada)
  }
  
  function getFiltroFinalizadas() {
    return estado.tarefas.filter(item => item.finalizada)
  }
  
const getFiltroTarefas = () => {
  const { filtro } = estado;
  
  switch (filtro) {
    case 'pendentes':
      return getFiltroPendentes();
    case 'finalizadas':
      return getFiltroFinalizadas()
    default: 
      return estado.tarefas;
  }
}

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes()"/>
    <Formulario
      :trocarFiltro = "e => estado.filtro = e.target.value" 
      :nova-tarefa = "e => estado.novaTarefa = e.target.value"
      :cadastra-tarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas="getFiltroTarefas()"/>
  </div>

</template>

<style scoped></style>
