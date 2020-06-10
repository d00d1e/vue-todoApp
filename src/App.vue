<template>
  <div id="app">
    <img class="logo" alt="Vue logo" src="./assets/logo.png">
    <div class="todo-list">
      <input type="text" class="todo-input" v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Create a new to-do">
        <li class="todo-item" v-for="todo in todos" :key="todo.id">
          <div class="edit" v-if="todo.edit">
            <input type="text" class="edit-input" v-model="todo.label" @keydown.enter="saveEdit(todo)">
          </div>
          <div class="view" v-else>
            <input type="checkbox" v-model="todo.completed" autofocus>
            &nbsp; 
            <del v-if="todo.completed" >{{ todo.label }}</del>
            <span v-else @dblclick="editTodo(todo)">{{ todo.label }}</span>
          </div>
          <div class="delete-button" @click="removeTodo(todo)">&times;</div>
        </li>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        todos: [
          { id: 0, label: 'Feed the cat', completed: true, edit: false},
          { id: 1, label: 'Do laundry', completed: false, edit: false},
          { id: 2, label: 'Finish Vue.js Todo App', completed: false, edit: false}
        ],
        currentTodo: '',
        editing: false
      };
    },
    methods: {
      addTodo() {
        if(this.currentTodo.trim().length === 0) {
          return
        }
        this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false, edit: false});
        this.currentTodo='';
      },
      completeTodo(todo) {
        todo.completed = !todo.completed;
      },
      editTodo(todo) {
        var index = this.todos.indexOf(todo);
        this.editedTodo = index;
        this.todos[index].edit = true;
      },
      saveEdit(todo) {
        var index = this.todos.indexOf(todo);
        this.todos[index].edit = false;
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

#app {
  font-family: 'Roboto Mono', monospace, Helvetica, Arial, sans-serif;
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

.edit-input {
  width: 300%;
  padding: 10px 10px;
  font-size: 14px;
  margin-bottom: 16px;
  font-family: 'Roboto Mono', monospace;
}

.todo-input {
  width: 100%;
  padding: 10px 10px;
  font-size: 18px;
  margin-bottom: 16px;
  font-family: 'Roboto Mono', monospace;
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
  text-align: right;
}

</style>
