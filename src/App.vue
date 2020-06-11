<template>
  <div id="app">

      <img id="logo" alt="Vue logo" src="./assets/logo.png">
       
      <div class="todo-list">
        <md-field>
          <md-input class="todo-input" v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Create a new to-do"></md-input>
        </md-field>

        <md-list class="todo-item">
          <li v-for="todo in todos" :key="todo.id">
          <md-card class="card">
            
            <div class="edit" v-if="todo.edit">
              <md-field>
                <md-input class="edit-input" v-model="todo.label" @keydown.enter="saveEdit(todo)"></md-input>
              </md-field>
            </div>

            <div class="view" v-else>
              <md-checkbox v-model="todo.completed" autofocus></md-checkbox>
              <del v-if="todo.completed" >{{ todo.label }}</del>
              <span v-else @dblclick="editTodo(todo)">{{ todo.label }}</span>
            </div>

            <md-button class="delete-button" @click="removeTodo(todo)">&times;</md-button>
          </md-card>
          </li>
        </md-list>
      </div>
  
  </div>
</template>

<script>
  export default {
    data() {
      return {
        todos: [
          { id: 0, label: 'Eat', completed: true, edit: false},
          { id: 1, label: 'Sleep', completed: false, edit: false},
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

#logo {
  display: block;
  margin: 30px auto;
  height: 75px;
}

.edit-input {
  width: 450px;
  padding-left: 20px;
}

.card {
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding-left: 30px;
}
</style>
