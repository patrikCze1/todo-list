<template>
  <div class="wrapper">
    <header>Todo list</header>
    <div class="inputField">
      <input v-model="todoName" v-on:keyup.enter="addTodo" placeholder="Add your new todo">
      <button v-on:click="addTodo"><i class="fas fa-plus"></i></button>
    </div>

    <ul class="todoList">
      <Todo v-for="todo in todos" :key="todo.id" :todoItem="todo"></Todo>
    </ul>

    <!-- <div class="footer">
      <span>You have <span class="pendingTasks"></span> pending tasks</span>
      <button>Clear All</button>
    </div> -->
  </div>

</template>

<script>
import Todo from './components/TodoItem.vue'

export default {
  name: 'App',
  components: {
    Todo,
  },
  data() { 
    return {
      todoName: '',
      todos: [],
    }
  },
  methods: {
    addTodo: function() {
      if (this.todoName.length > 0) {
        this.todos.push({'id': Date.now(), 'text': this.todoName, 'completed': false });
        this.todoName = '';
        this.save();
      }
    },
    removeTodo: function(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
      this.save();
    },
    save: function() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    load: function() {
      const todos = localStorage.getItem('todos');
      if (todos)
        this.todos = JSON.parse(todos);
    }
  },
  mounted() {
    this.load();
  },
  props: {
    Todo: Object
  }
}
</script>

<style>

</style>
