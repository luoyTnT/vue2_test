<template>
  <ul class="todo-main">
    <MyListItem
      v-for="todoObj in todos"
      :key="todoObj.id"
      :todo="todoObj"
      :checkTodo="checkTodo"
      :removeTodo="removeTodo"
    />
  </ul>
</template>

<script>
import MyListItem from "./MyListItem";

export default {
  name: "MyList",
  props: ["todos", "checkTodo", "removeTodo"],
  components: { MyListItem },
};
</script>

<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>