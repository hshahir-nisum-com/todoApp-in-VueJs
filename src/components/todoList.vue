<template>
  <div class="list-container">
    <ul>
      <li
        class="li-item todo-list-item"
        type="text"
        name="todoList"
        v-for="(item, index) in items"
        :class="{ completed: item.complete }"
        :key="item"
      >
        {{ item.todo }}
        <input
          type="button"
          value="Delete"
          class="btn-dlt"
          v-on:click="onDelete(index)"
        />
        <input
          type="checkbox"
          name="checkBox"
          class="checkBox"
          id="checkBox"
          v-on:change="onChange($event, index)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "todoList",
  props: {
    items: {
      required: true,
    },
  },
  data() {
    return {
      whenUpdate: false,
    };
  },
  methods: {
    onChange: function (event, ind) {
      this.$emit("checked", event.target.checked, ind);
    },
    onDelete(ind) {
      console.log("dlt :", ind);
      this.$emit("onDelete", ind);
    },
  },
};
</script>

<style scoped>
.todo-list-item {
  border: 0;
  text-align: left;
  -moz-appearance: textfield;
  -webkit-appearance: textfield;
  background-color: white;
  background-color: -moz-field;
  font-size: 25px;
}
.li-item {
  list-style-type: none;
}
.list-container {
  text-align: left;
  margin: 0 auto;
  width: 600px;
  padding: 0;
}
ul {
  padding: 0;
}
.checkBox {
  /* font-size: 85px; */
  transform: scale(1.5);
  float: right;
  margin-top: 8px;
  margin-right: 10px;
}
.btn-dlt {
  float: right;
  margin-top: 4px;
}
.completed {
  text-decoration: line-through;
}
</style>