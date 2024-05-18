<script setup>
const props = defineProps(['cadastraTarefa', 'tarefaTemporaria', 'trocarFiltro', 'editaTarefaTemporaria'])
</script>

<template>

    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemporaria" @change="props.editaTarefaTemporaria" required type="text"
                    placeholder="Digite aqui a descrição da tarefa" class="form-control">
            </div>

            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>

            <div class="col-md-2">
                <select class="form-control" @change="props.trocarFiltro">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>