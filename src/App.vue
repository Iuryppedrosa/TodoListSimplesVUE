<template>
  <div class="todo-list">
    <h1>Lista de Tarefas</h1>
    <!-- @sumit. -->
    <!--forma abreveada de v-on:submit, o prevent, previne o submit de carregar a pagina-->
    <form v-on:submit.prevent="addTask">
      <!-- v-model liga a propriedade do dado -->
      <input v-model="newTask" placeholder="Nova tarefa" />
      <button type="submit">Adicionar</button>
    </form>
    <ul>
      <!-- v-for itera sobre a lista de task, passando um index -->
      <li
        v-for="(task, index) in tasks"
        :key="index"
        :class="{
          completed: task.completed,
        }"
      >
        <input type="checkbox" v-model="task.completed" />
        <span> {{ task.text }}</span>
        <!-- v-on:click -->
        <!-- @evento=metodo -->
        <button @click="removeTask(index)">Remover</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [
        { text: "Aprender Vue.js", completed: false },
        { text: "Aprender React", completed: false },
        { text: "Aprender Angular", completed: false },
      ],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push({
          text: this.newTask,
          completed: false,
        });
        this.newTask = "";
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style>
.todo-list {
  max-width: 400px;
  margin: 0 auto;
  text-align: center;
}

.completed span {
  text-decoration: line-through;
}

input[type="text"] {
  width: 70%;
  padding: 0.5em;
  margin-right: 0.5em;
}

button {
  padding: 0.5em;
  cursor: pointer;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.5em 0;
}
</style>
