<template>
  <div>
    <md-card>
    <Header/>
    <md-field>
    <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add item here">
    </md-input>
    </md-field>
      <ul class="todos">
      <li class="todo-item" v-for="todo in todos" :key="todo.id">
        <input class="completed" type="checkbox" @change="togglecompleted" v-model="todo.completed"/>
        <span v-if="todo.editing === false" class="editing" :class="{editing: todo == editedTodo}" @dblclick="editTodo(todo)">
          {{ todo.label }}
        </span>
        <md-field v-if="todo.editing" class="editing">
          <md-input
                  type="text"
                  v-model="todo.label"
                  @keyup.enter="stopEdit(todo)"
                  @keyup.esc="stopEdit(todo)"
                  @focusout="stopEdit(todo)"
                  placeholder="Add item here"
          />
        </md-field>
        <button v-if="todo.editing === false" @click="editTodo(todo)">Edit</button>
        <button v-if="todo.editing === true" @click="stopEdit(todo)">Save</button>
        <button v-if="todo.editing === false" @click="removeTodo(todo)">Delete</button>
        <button v-if="todo.editing === true" @click="editTodo(todo)">Cancel</button>
      </li>
    </ul>
    </md-card>
  </div>
</template>

<script>
import Header from './components/layout/Header';
export default {
  components: {
    Header
  },
  data() {
    return {
      todos: [],
      currentTodo: '',
      editedTodo: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false, editing: false});
      this.currentTodo = '';
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      const index = this.todos.indexOf(todo);
      this.todos[index].editing = !this.todos[index].editing;
    },
    stopEdit(todo) {
      todo.editing = false;
    }
  }
};
</script>

<style>

  body {
    font-family: 'Roboto', sans-serif;
    font-size: 20px !important;
    line-height: 1.4 !important;
    margin-left: 30px !important;
    margin-right: 30px !important;
    background-color: #ffffff;
    background-color: #ffffff;
    background-color: #ffffff;
    background-color: #ffffff;
    background-image: url("data:image/svg+xml,%3Csvg width='42' height='44' viewBox='0 0 42 44' xmlns='http://www.w3.org/2000/svg'%3E%3Cg id='Page-1' fill='none' fill-rule='evenodd'%3E%3Cg id='brick-wall' fill='%2384c2ea' fill-opacity='0.4'%3E%3Cpath d='M0 0h42v44H0V0zm1 1h40v20H1V1zM0 23h20v20H0V23zm22 0h20v20H22V23z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
  }

  .md-card {
    width: 50% !important;
    margin-left: auto;
    margin-right: auto;
    margin-top: 20px;
    background-color: #ffffff !important;
  }

  ul {
    list-style-type: none;
    margin-left: 0px;
    padding: 0;
  }

  div {
    padding-bottom: 10px !important;
    padding-left: 30px !important;
  }

  placeholder {
    font-style: italic;
  }

  button {
    margin: 3px;
  }

  span {
    padding-left: 3px !important;
    padding-right: 3px !important;
  }

  .editing {
    display: inline-block !important;
    border: none !important;
    border-radius: 5px !important;
    height: 35px;
    font-size: 20px !important;
  }

  .completed {
    width: 17px !important;
    height: 17px !important;
  }

  .md-field {
    border: 2px solid lightblue !important;
    height: 40px !important;
    border-radius: 5px !important;
    width: 60% !important;
    font-size: 20px !important;
    min-height: 0px !important;
    font-size: 20px !important;
    padding-top: 5px !important;
    padding-left: 5px !important;
  }

  .md-input {
    width: 66% !important;
  }

  @media (max-width: 768px) {
    .md-card {
      width: 100% !important;
    }

  }

</style>
