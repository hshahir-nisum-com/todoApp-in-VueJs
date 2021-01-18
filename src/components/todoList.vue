<template>
  <div class="list-container">
    <ul>
      <li
        class="li-item todo-list-item"
        type="text"
        name="todoList"
        :contenteditable="editable"
        v-for="(item, index) in items"
        v-on:click="clickedToEdit($event, index)"
        :key="item"
      >
        {{ item.todo }}
        <input
          type="button"
          value="UPDATE"
          :class="{ updatedButton: whenUpdate }"
          class="btn-update"
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
      editable: false,
      whenUpdate: false,
    };
  },
  methods: {
    onChange: function (event, ind) {
      this.$emit("checked", event.target.checked, ind);
    },
    clickedToEdit: function (event, ind) {
      this.editable = true;
      this.whenUpdate = true;
      let element = event.target;
      let observer = new MutationObserver((mutations) =>
        mutations.forEach((mutation) => {
          this.$emit("onUpdate", mutation.target.data, ind);
          console.log("input changed", mutation.target.data);
        })
      );
      observer.observe(element, {
        childList: true,
        characterData: true,
        subtree: true,
      });
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
}
.btn-update {
  display: none;
}
.updatedButton {
  display: inline;
  float: right;
  margin-top: 4px;
}
</style>