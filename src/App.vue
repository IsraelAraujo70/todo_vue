<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({
    filtro: 'Todas' ,
    tarefaTemp: '',
    tarefas : [
      {
        titulo: 'Estudar ES6',
        finalizada: false
      },
      {
        titulo: 'Estudar Sass',
        finalizada: false
      },
      {
        titulo: 'Ir para academia',
        finalizada: true
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
  }

  const getTarefasFilanizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
  }

  const getTarefasFiltradas = () =>{
    const {filtro} = estado
    switch (filtro){
      case 'pendentes':
        return getTarefasPendentes()
      case 'finalizadas':
      return getTarefasFilanizadas()
      default:
        return estado.tarefas
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = ''
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"></Cabecalho>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefaTemp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa ="cadastraTarefa"></Formulario>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"></ListaDeTarefas>
  </div>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
