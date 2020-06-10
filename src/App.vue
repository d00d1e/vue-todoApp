<template>
  <div id="app-container">
    <img class="logo" alt="Vue logo" src="./assets/logo.png">
    <div class="todo-list">
      <input type="text" class="todo-input" v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Create a new to-do">

      <div class="todo-item-list">
        
        <li class="todo-item" v-for="todo in todos" :key="todo.id">
          <input type="checkbox" v-model="todo.done" autofocus>
          <del v-if="todo.done">{{ todo.label }}</del>
          <span v-else>{{ todo.label }}</span>

          <button class="delete-button" @click="removeTodo(todo)">&times;</button>
        
        </li>

      </div> 
        
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        todos: [
          { id: 0, label: 'Feed the cat', done: true},
          { id: 1, label: 'Do laundry', done: false},
          { id: 2, label: 'Finish Vue.js', done: false}
        ],
        currentTodo: '', 
        editing: null
      };
    },
    methods: {
      addTodo() {
        if(this.currentTodo.trim().length === 0) {
          return
        }
        this.todos.push({id: this.todos.length, label: this.currentTodo, done: false});
        this.currentTodo='';
      },
      completeTodo(todo) {
        todo.done = !todo.done;
      },
      removeTodo(todo) {
        var index = this.todos.indexOf(todo);
        this.todos.splice(index, 1);
      }
    }
  };
</script>

<style>
* {
  box-sizing: border-box;
}

#app-container {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 18px;
  max-width: 600px;
  margin: 0 auto;
}

.logo {
  display: block;
  margin: 20px auto;
  height: 75px;
}

.todo-input {
  width: 100%;
  padding: 10px 10px;
  font-size: 18px;
  margin-bottom: 16px;
}

.todo-item {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.delete-button {
  cursor: pointer;
  margin-left: 14px;
  
}

</style>
