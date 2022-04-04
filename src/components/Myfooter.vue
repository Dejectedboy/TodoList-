<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" :checked="isAll" @change="checkAll" />
    </label>
    <span>
      <span>待完成{{ doneTotal }}</span> / 已完成{{ total }}
    </span>
    <button class="btn btn-danger" @click="cleartodo">清除已完成的任务</button>
  </div>
</template>

<script>
export default {
  name: "Myfooter",
  props: ["tomembers", "checkAllTodo", "clearTodo"],
  computed: {
    doneTotal() {
      // let i = 0;
      // this.tomembers.forEach((todo) => {
      //   if (todo.done) i++;
      // });
      // return i;
      return this.tomembers.reduce(
        (pre, current) => pre + (current.done ? 1 : 0),
        0
      );
    },
    total() {
      return this.tomembers.length;
    },
    isAll() {
      return this.total === this.doneTotal && this.total > 0;
    },
  },
  methods: {
    checkAll(e) {
      this.checkAllTodo(e.target.checked);
    },
    cleartodo() {
      this.clearTodo();
    },
  },
};
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
