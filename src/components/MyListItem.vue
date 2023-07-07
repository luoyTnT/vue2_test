<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todo.done"
        @change="handleCheck(todo.id)"
      />
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input
        type="text"
        v-show="todo.isEdit"
        :value="todo.title"
        @blur="handleBlur(todo, $event)"
        ref="inputTitle"
      />
    </label>
    <button class="btn btn-danger" @click="handleRemoveTodo(todo.id)">
      删除
    </button>
    <button class="btn btn-edit" @click="handleEditTodo(todo)" v-show="!todo.isEdit">修改</button>
  </li>
</template>

<script>
export default {
  name: "MyListItem",
  props: ["todo", "checkTodo", "removeTodo"],
  methods: {
    handleCheck(id) {
      this.checkTodo(id);
    },
    handleRemoveTodo(id) {
      if (confirm("确定要删除吗？")) {
        this.removeTodo(id);
      }
    },
    handleEditTodo(todo) {
      if (todo.hasOwnProperty("isEdit")) {
        todo.isEdit = true;
      } else {
        this.$set(todo, "isEdit", true);
      }
      this.$nextTick(function () {
        this.$refs.inputTitle.focus();
      });
    },
    handleBlur(todo, element) {
      todo.isEdit = false;
      if (!element.target.value.trim()) {
        return alert("修改值不能为空！");
      }
      this.$bus.$emit("updateTodo", todo.id, element.target.value);
    },
  },
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover button {
  display: block;
}
</style>