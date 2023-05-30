<template>
  <main class="app d-flex justify-content-center">
    <div class="container">
      <form @submit.prevent="addTodo">
        <div class="d-flex justify-content-center">
          <input type="text" autocomplete="off" name="task" v-model="task" />
          <button type="submit">ADD</button>
        </div>
      </form>
      <to-do v-for="(todo, index) of todos" :todo="todo" :index="index" @deleteTask="deleteTask"></to-do>
    </div>
  </main>
</template>

<script>
import ToDo from './components/ToDo.vue';

export default {
  name: "App",
  components: {
    ToDo,
  },
  data: function () {
    return {
      todos: [],
      task: '',
      lastId: 0
    }
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem('todos')) || [];
  },
  watch: {
    todos: {
      handler(newValue) {
        localStorage.setItem('todos', JSON.stringify(newValue));
      },
      deep: true
    }
  },
  methods: {
    addTodo() {
      if (this.task.trim() === '') {
        this.task = '';
        return;
      }

      this.todos.push({
        text: this.task,
        status: false,
        id: ++this.lastId
      });
      this.task = '';
    },
    deleteTask(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
};
</script>
