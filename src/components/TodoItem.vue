<template>
  <div>
    <li
      :style="{ background: bgColor }"
      @mouseenter="handleEnter(false)"
      @mouseleave="handleEnter(true)"
    >
      <label>
        <input type="checkbox" :checked="todo.done" @change="change(todo.id)" />
        <span>{{ todo.title }}</span>
      </label>
      <button class="btn btn-danger" v-show="isShow" @click="deleteItem()">
        删除
      </button>
    </li>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  data() {
    return {
      isShow: false,
      bgColor: "white",
    };
  },
  props: {
    todo: {
      type: Object,
    },
    deleteTodo: {
      type: Function,
    },
    index: {
      type: Number,
    },
    updateChecked: {
      type: Function,
    },
  },
  methods: {
    deleteItem() {
      const { index, todo, deleteTodo } = this;
      if (window.confirm(`确定删除${todo.title}吗？`)) {
        deleteTodo(index);
      }
    },
    handleEnter(isEnter) {
      if (isEnter) {
        this.isShow = true;
        this.bgColor = "#aaa";
      }
    },
    change(id) {
      this.updateChecked(id);
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
li:hover {
  background-color: #dddddd;
}
li:hover button {
  display: block;
}
</style>