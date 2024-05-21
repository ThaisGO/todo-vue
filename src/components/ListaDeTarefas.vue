<script setup>
    const props = defineProps(['tarefas'])
</script>

<template>
    <ul class="list-group mt-4" v-if="props.tarefas.length > 0">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input type="checkbox" @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo">
            <label :class="{ done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
        </li>
    </ul>

    <div class="d-flex justify-content-center pt-4" v-if="props.tarefas.length === 0">
        <p class="fs-2">Adicione novas tarefas na sua agenda!</p>
    </div>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>