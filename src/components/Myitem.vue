<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todos.done"
        @click="handleCheck(todos.id)"
      />
      <!-- 如下代码也能实现功能，但不太推荐，因为有点违反原则，修改了props -->
      <!-- <input type="checkbox" :checked="todos.done" v-model="todos.done" /> -->
      <span>{{ todos.name }}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todos.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: "Myitem",
  props: ["todos", "checkTodo", "deleteTodo"],
  methods: {
    handleCheck(id) {
      this.checkTodo(id);
    },
    handleDelete(id) {
      if (confirm("确定要删除吗")) {
        //通知app删除所点击的li对象
        this.deleteTodo(id);
      }
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
  /* background: #ddd; */
  display: block;
}
li:hover {
  background: #ddd;
}
</style>
