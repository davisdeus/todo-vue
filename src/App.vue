<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemporario: '',
    tarefas: [
      {
        titulo:'Estudar ES6',
        finalizada: false
      },
      {
        titulo:'Estudar SASS',
        finalizada: false
      },
      {
        titulo:'Ir parar academia',
        finalizada: true
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada )
  }
  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }
  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
        case 'finalizadas':
          return getTarefasFinalizadas();
          default:
            return estado.tarefas;
    }
  }

  const cadastrarTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemporario,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemporario = '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendens
      </p>
    </header>

    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemporario" @change="evento => estado.tarefaTemporario = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>

        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>

        <div class="col-md-2">
          <section class="form-control" @change="evento => estado.filtro = evento.target.value">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">pendentes</option>
            <option value="finalizadas">finalizadas</option>
          </section>
        </div>
      </div>
    </form>
    
    <ul class="list-grup">
      <li class="list-grup-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
  
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
