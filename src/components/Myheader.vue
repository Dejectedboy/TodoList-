<template>
  <div class="todo-header">
    <input
      type="text"
      placeholder="添加所需完成的任务"
      @keyup.enter="enter"
      v-model="name"
    />
  </div>
</template>

<script>
import { nanoid } from "nanoid";
export default {
  name: "Myheader",
  data() {
    return {
      name: "",
    };
  },

  methods: {
    enter(e) {
      if (!this.name.trim()) return alert("输入不能为空");
      //将用户包装成一个todo对象
      const member = { id: nanoid(), name: this.name, done: false };
      //数据传到父组件app上
      this.add(member);
      //清空输入
      this.name = "";
    },
  },
  props: ["add"],
};
</script>

<style scoped>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}
.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
