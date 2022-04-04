<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <Myheader :add="addmembers" />
        <MyList
          :tomembers="members"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        />
        <Myfooter
          :tomembers="members"
          :checkAllTodo="checkAllTodo"
          :clearTodo="clearTodo"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Myheader from "./components/Myheader.vue";
import Myfooter from "./components/Myfooter.vue";
import MyList from "./components/Mylist.vue";

export default {
  name: "App",
  data() {
    return {
      members: JSON.parse(localStorage.getItem("members")) || [],
    };
  },

  methods: {
    addmembers(member) {
      this.members.unshift(member);
    },

    checkTodo(id) {
      //遍历进行数据取反点击之后，当前的id值与原本id值一样，进行取反
      this.members.forEach((e) => {
        if (e.id === id) e.done = !e.done;
      });
    },

    deleteTodo(id) {
      //过滤掉与点击id相同id的一组对象(内容)
      this.members = this.members.filter((member) => {
        return member.id !== id;
      });
    },
    //全选or取消全选
    checkAllTodo(check) {
      this.members.forEach((member) => {
        member.done = check;
      });
    },
    //清除所有勾选
    clearTodo() {
      this.members = this.members.filter((member) => {
        return !member.done;
      });
    },
  },

  components: {
    Myheader,
    Myfooter,
    MyList,
  },
  watch: {
    members: {
      deep: true,
      handler(value) {
        localStorage.setItem("members", JSON.stringify(value));
      },
    },
  },
};
</script>

<style>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>