<template>

  <transition
      name="custom-classes-transition"
      enter-active-class="animated tada"
      leave-active-class="animated bounceOutRight"
    >
    <li v-if="show" class="" v-bind:class="{'completed': todo.completed}"> 
      <span class="check" v-on:click="completeTodo"><i class="fas fa-check-circle"></i></span>
      <input v-model="todo.text" class="todo-input">
      <!-- <span v-on:click="completeTodo">{{ todo.text }}</span> -->
      <span class="icon" v-on:click="remove" @click="show = !show"><i class="fas fa-trash-alt"></i></span> 
    </li>  
  </transition>
  
</template>

<script>

export default {
  name: 'Todo',
  props: {
    todoItem: Object
  },
  data() {
    return {
      todo: this.todoItem,
      show: true,
    }
  },
  methods: {
    completeTodo: function() {
      this.todo.completed = !this.todo.completed;
    },
    remove: function() {
      setInterval(() => {
        this.$parent.removeTodo(this.todo.id);
      }, 600);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
