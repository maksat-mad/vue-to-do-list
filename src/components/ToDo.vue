<template>
    <div class="task d-flex justify-content-center align-items-center">
        <p v-bind:class="todo.status ? 'text-decoration-line-through' : ''">{{ (index + 1) + '. ' + todo.text }}</p>
        <button @click="changeStatus">{{ todo.status ? 'Not Done' : 'Done' }}</button>
        <button @click="deleteTask">&times;</button>
    </div>
</template>

<script>
export default {
  props: ['todo', 'index'],
  mounted() {
    this.emit = this.$emit;
  },
  methods: {
    changeStatus() {
        this.todo.status = !this.todo.status;
    },
    deleteTask() {
        this.emit('deleteTask', this.todo.id);
    }
  }
}
</script>
