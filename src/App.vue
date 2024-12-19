<script setup>
  import { ref } from 'vue';
  import claus from './assets/download.gif';
  import claus2 from './assets/download (1).gif';

  const tarefas = ref([
    "Arrumar a cama",
    "Estudar",
    "Treinar"
  ]);

  const tarefasConcluida = ref([]);

  function remover(i) {
    tarefas.value.splice(i, 1);
  }

  function removerTarefaConcluida(i) {
    tarefasConcluida.value.splice(i, 1);
  }

  const novaTarefa = ref("");

  function adicionar() {
    if (novaTarefa.value.trim() !== "") {
      tarefas.value.push(novaTarefa.value.trim());
      novaTarefa.value = "";
    }
  }

  function concluir(tarefa) {
   // Encontra a tarefa nas pendentes e a remove
   remover(tarefas.value.indexOf(tarefa)); 

    // Adiciona a tarefa na lista de tarefas concluídas
    tarefasConcluida.value.push(tarefa);
  }
</script>

<template>
  <main>
    <h1>📌ToDo List</h1>
    <section class="add">
      <input type="text" placeholder="digite uma tarefa" v-model="novaTarefa">
      <button @click="adicionar">Adicionar</button>
    </section>
    <div class = "task" v-if="tarefas.length === 0">
      <p>Você completou todas as tarefas!</p>
      <img :src="claus" alt="Papai Noel" />
    </div>
    <ul v-else>
      <!-- tarefa = string inteira, i = index -->
      <li v-for="(tarefa, i) in tarefas" :key="i">
        {{ tarefa }}
        <div>
          <button @click="remover(i)">❌</button>
          <button @click="concluir(tarefa)">✔️</button>
        </div>
      </li>
    </ul>

    <section>
      <h2>Tarefas Concluídas</h2>
      <div class = "nenhumatask" v-if="tarefasConcluida.length === 0">
        <p>Nenhuma tarefa completa!</p>
        <img :src="claus2" alt="Papai Noel" />
      </div>
      <ul v-else>
        <li v-for="(tarefa, i) in tarefasConcluida" :key="i">
          {{ tarefa }}
          <button @click="removerTarefaConcluida(i)">❌</button>
        </li>
      </ul>
    </section>
  </main>
</template>

<style lang="scss">
main {
  margin: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: start;
  height: 80vh;
  width: 40vw;
  background-color: #a62f24;
  border-radius: 24px;

  h1,h2{
    color: white;
    font-family: monospace;
    font-weight: bolder;
    font-size: 2.2em;
  }

  p{
    color: white;
    font-family: monospace;
  }
}

body {
  background-image: url('src/assets/xmasArvore.jpg');
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

li{
  display: flex;
  justify-content: space-around;
  align-items: center;
  list-style: none;
  width: 20vw;
  height: 5vh;
  border-radius: 8px;
  background-color: #F2EBDC;
  margin: 1.5vh 0;
  transition: transform 0.3s ease;
  cursor: default;

  &:hover {
    transform: scale(1.05);
  }

}

button { 
    background-color: #a6bd83;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

.add{
  width: 25vw;
  display: flex;
  justify-content: end;

  input{
    padding: 1.2vh;
    width: 16vw;
    border-radius: 8px;
    border: none;
    margin: 0 8px;
  }
}

.nenhumatask{
  display: flex;
  justify-content: space-between;

  img{
   width: 8vw;
  }
}

.task{
  display: flex;
  justify-content: space-between;

  img{
   width: 5vw;
  }
}
</style>
