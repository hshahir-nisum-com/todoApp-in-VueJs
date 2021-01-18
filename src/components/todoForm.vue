<template>
  <div class="form-container">
    <h1>Todo App</h1>
    <form class="form">
      <label class="todo-label">New Todo</label>
      <input
        type="text"
        v-model="newTodo"
        name="newTodo"
        placeholder="Enter Your todos"
        class="txtBox"
        autocomplete="off"
        
      />
      <input type="button" value="Add todo" class="btn" @click="addTodo()" />
    </form>
  </div>
  
    <todo-list v-bind:items="todoListItem" @checked="onComplete"  @onUpdate = "toUpdate"/>
  
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
        this.todoListItem.push({todo:this.newTodo,
                                complete : false});
      }
      this.newTodo = null;
    },
    onComplete(flag, ind){
      this.todoListItem[ind].complete = flag
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
  margin: 10px 0;
}

.txtBox {
  width: 470px;
  height: 50px;
  border-radius: 5px;
  margin-right: 20px;
  font-size: 20px;
}

.btn {
  width: 100px;
  height: 30px;
  font-size: 20px;
  border-radius: 2px;
}
</style>
