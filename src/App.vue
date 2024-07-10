<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <TodoHeader :addTodo="addTodo"/>
      <TodoList :todos="todos" :deleteTodo="deleteTodo" :updateChecked="updateChecked"/>
      <TodoFooter />
    </div>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  name: 'App',
  components: {
    TodoHeader,
    TodoList,
    TodoFooter
  },
  data() {
    return {
      todos:[
        {id:'001',title:'吃饭',done:true},
        {id:'002',title:'睡觉',done:false},
        {id:'003',title:'打豆豆',done:true}]
    }
  },
  methods: {
    // 添加todo
    addTodo(todo) {
      this.todos.unshift(todo)
    },
    deleteTodo(index){
      this.todos.splice(index,1)
    },
    // 更新选中状态
    updateChecked(id) {
      this.todos.forEach(e => {
        if (e.id === id) {
          e.done = !e.done
        }
      })
    }
  }
}
</script>

<style>
/*app*/
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
