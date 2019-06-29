<template>
  <div class id="app">
    <div class="container grid-xs py-2">
      <img class="img-responsive img-logo" src="@/assets/lista.png" width="112px" alt="list" />
      <form @submit.prevent="addToDo(todo)">
        <div class="input-group">
          <input type="text" v-model="todo.description" class="form-input" placeholder="new to do" />
          <button class="btn btn-primary input-group-btn">add</button>
        </div>
      </form>
      <div class="todo-list">
        <todo v-for="t in todos" :key="t.id" @toggle="toggleToDo" @remove="removeToDo" :todo="t" />
      </div>
    </div>
  </div>
</template>

<script>
import Todo from "./components/Todo";

export default {
  name: "app",
  components: { Todo },
  data() {
    return { todos: [], todo: { checked: false } };
  },
  methods: {
    addToDo(todo) {
      todo.id = Date.now();
      this.todos.push(todo);
      this.todo = { checked: false };
    },
    toggleToDo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id);
      if (index > -1) {
        const checked = !this.todos[index].checked;
        this.$set(this.todos, index, { ...this.todos[index], checked });
      }
    },

    removeToDo(todo){
      const index = this.todos.findIndex(item => item.id === todo.id);
      if(index > -1){
        this.$delete(this.todos, index)
      }
    }
  }
};
</script>

<style scoped>
.img-logo {
  max-width: 200px;
  margin: 0 auto;
}

.todo-list {
  padding-top: 2rem;
}
</style>
