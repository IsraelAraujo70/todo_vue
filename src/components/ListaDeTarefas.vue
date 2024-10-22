<script setup>
    const props = defineProps([
        'tarefas'
    ])
</script>
<template>
    <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :for="tarefa.titulo" class="ms-3" :class="{done: tarefa.finalizada}">
        {{tarefa.titulo}}
        </label>
    </li>
    </ul>
</template>