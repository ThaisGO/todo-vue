<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  newTask: '',
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
    titulo: estado.newTask,
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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{  getTarefasPendentes() }} tarefas</p>
    </header>
    
    <form @submit.prevent="cadastraTarefa()">
      <div class="row">
        <div class="col-md-9">
          <input 
            @change="e => estado.newTask = e.target.value"
            type="text" 
            class="form-control" 
            placeholder="Digite a descrição da tarefa">
        </div>
  
        <div class="col-md-1">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="e => estado.filtro = e.target.value">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getFiltroTarefas()">
        <input type="checkbox"
          @change="e => tarefa.finalizada = e.target.checked"
          :checked="tarefa.finalizada" 
          :id="tarefa.titulo">
        <label :class="{ done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>

</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
