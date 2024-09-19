<template>
  <v-container>
    <v-row class="text-center" justify="center">
      <v-col cols="12" sm="8" md="6">
        <v-card class="todo-card" outlined>
          <v-card-title>
            <v-text-field
              v-model="newTodo"
              label="Add a new task"
              @keyup.enter="addTodo"
              solo
            ></v-text-field>
          </v-card-title>

          <v-list>
            <v-list-item-group v-for="(todo, index) in todos" :key="index">
              <v-list-item>
                <v-row align="center" no-gutters>
                  <v-col cols="8" class="text-left px-2 py-4">
                    <v-list-item-title>{{ todo.text }}</v-list-item-title>
                  </v-col>
                  <v-col cols="4" class="text-right">
                    <v-btn @click="editTodo(index)" icon>
                      <v-icon>mdi-pencil</v-icon>
                    </v-btn>
                    <v-btn @click="deleteTodo(index)" icon>
                      <v-icon>mdi-delete</v-icon>
                    </v-btn>
                  </v-col>
                </v-row>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      newTodo: '',
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({ text: this.newTodo });
        this.newTodo = '';
      }
    },
    editTodo(index) {
      const updatedTodo = prompt('Edit your task:', this.todos[index].text);
      if (updatedTodo !== null) {
        this.todos[index].text = updatedTodo;
      }
    },
    deleteTodo(index) {
      if (confirm('Are you sure you want to delete this task?')) {
        this.todos.splice(index, 1);
      }
    },
  },
};
</script>

<style scoped>
.todo-card {
  width: 400px;
  margin: 20px auto;
}

.v-list-item {
  margin-bottom: 8px;
}

.v-btn {
  margin-left: 5px;
}
</style>
