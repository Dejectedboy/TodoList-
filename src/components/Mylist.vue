<template>
  <ul class="todo-main">
    <Myitem
      v-for="member in tomembers"
      :key="member.id"
      :todos="member"
      :checkTodo="checkTodo"
      :deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script>
import Myitem from "./Myitem.vue";
export default {
  name: "MyList",
  components: {
    Myitem,
  },

  props: ["tomembers", "checkTodo", "deleteTodo"],
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
