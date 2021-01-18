<template>
  <div class="form-container">
    <h1>Todo App</h1>
    <form class="form" @submit.prevent="submit">
      <label class="todo-label">New Todo</label>
      <input
        type="text"
        v-model="newTodo"
        name="newTodo"
        placeholder="Enter Your todos"
        class="txtBox"
        autocomplete="off"
        @keyup.enter="addTodo()"
      />
      <input type="button" value="Add todo" class="btn" @click="addTodo()" />
    </form>
  </div>

  <todo-list
    v-bind:items="todoListItem"
    @checked="onComplete"
    @onDelete="toDelete"
  />
</template>

<script>
import TodoList from "./todoList";
export default {
  name: "formTodo",
  components: {
    TodoList,
  },
  data() {
    return {
      newTodo: null,
      todoListItem: [],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo != null) {
        this.todoListItem.push({ todo: this.newTodo, complete: false });
      }
      this.newTodo = null;
    },
    onComplete(flag, ind) {
      this.todoListItem[ind].complete = flag;
    },
    toDelete(ind) {
      console.log("from parent :", ind);
      this.todoListItem = this.todoListItem.filter(
        ({ todo }) => todo !== this.todoListItem[ind].todo
      );
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-container {
  width: fit-content;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  text-transform: uppercase;
  width: 600px;
}
.todo-label {
  display: block;
  text-align: left;
  margin: 10px 5px;
}

.txtBox {
  width: 470px;
  height: 50px;
  border-radius: 5px;
  margin-right: 5px;
  font-size: 20px;
  text-transform: uppercase;
  border-color: blue;
}

.btn {
  width: 115px;
  height: 55px;
  font-size: 20px;
  border-radius: 5px;
  text-transform: uppercase;
  background-color: blue;
  color: rgb(247, 245, 243);
  border: 0;
}
.btn:hover {
  background-color: rgb(108, 108, 247);
}
</style>
