<template>
  <div class="container">
    <md-card>
      <md-card-header class="header">
        <div class="md-title">My ToDo's</div>
      </md-card-header>
      <md-card-content>
        <md-field>
          <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Enter ToDo"></md-input>
        </md-field>
        <div class="todo-list">
          <ul class="todos">
            <li class="todo-item" v-for="todo in todos" :key="todo.id">
              <span>
                <input
                  class="completed"
                  type="checkbox"
                  @change="toggleCompleted"
                  v-model="todo.completed"
                />

                <span
                  v-if="todo.editing === false"
                  class="todo-item-label"
                  :class="{'is-complete': todo.completed}"
                  @dblclick="editTodo(todo)"
                >{{ todo.label }}</span>
                <div v-if="todo.editing">
                  <md-field>
                    <md-input
                      type="text"
                      v-model="todo.label"
                      @keyup.enter="stopEdit(todo)"
                      @keyup.esc="stopEdit(todo)"
                      @focusout="stopEdit(todo)"
                    ></md-input>
                  </md-field>
                </div>
              </span>
              <span class="actions">
                <md-button class="btn-edit" @click="editTodo(todo)">
                  <md-icon>edit</md-icon>
                </md-button>
                <md-button class="btn-delete" @click="removeTodo(todo)">
                  <md-icon>delete</md-icon>
                </md-button>
              </span>
            </li>
          </ul>
        </div>
      </md-card-content>
    </md-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      editedTodo: ""
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        editing: false
      });

      this.currentTodo = "";
    },
    toggleCompleted() {
      this.todo.completed = !this.todo.completed;
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.editing = true;
    },
    stopEdit(todo) {
      todo.editing = false;
    }
  }
};
</script>

<style>
.md-card {
  max-width: 800px;
  margin: 30px auto;
}
.header {
  text-align: center;
  background: #000000;
  color: white;
}
.md-title {
  font-size: 3em !important;
  color: #64c2ec;
}

.md-card-content {
  margin-left: 10px;
  font-size: 2em !important;
}
.md-field {
  min-width: 300px !important;
  max-width: 400px;
  border-bottom: 2px dotted;
  border-color: lightgray;
  font-size: 2em !important;
}
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.todo-item {
  margin-top: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 0.1px solid;
  border-color: lightgray;
}
.todo-item-label {
  margin-left: 10px;
}
.is-complete {
  text-decoration: line-through;
  color: lightgray;
}
.btn-edit {
  color: green;
}
.btn-delete {
  color: red;
}
</style>