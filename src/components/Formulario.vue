<script setup>
    const props = defineProps([
        'cadastraTarefa',
        'novaTarefa',
        'trocarFiltro'
    ])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col-md-9">
                <input 
                    @change="props.novaTarefa" 
                    type="text" 
                    class="form-control"
                    placeholder="Digite a descrição da tarefa">
                <!-- <input 
                    @change="e => estado.newTask = e.target.value" type="text" class="form-control"
                    placeholder="Digite a descrição da tarefa"> -->
            </div>

            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <!-- <select class="form-control" @change="e => estado.filtro = e.target.value"> -->
                <select class="form-control" @change="props.trocarFiltro">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>