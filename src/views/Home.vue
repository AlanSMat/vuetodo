<template>
  <div id="home">
    <AddToDo v-on:add-todo="addToDo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>
<script>
import Todos from "../components/Todos";
import AddToDo from "../components/AddToDo";
import axios from "axios";

export default {
  components: {
    Todos,
    AddToDo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(
          res =>
            (this.todos = this.todos.filter(todoItem => todoItem.id !== id))
        )
        .catch(err => console.log(err));
      // this.todos.map((item, i) => {
      //   if (item.id === id) {
      //     this.todos.splice(i, 1);
      //   }
      // });

      // ** better
      //this.todos.splice(this.todos.findIndex(todoItem => todoItem.id === id), 1);

      // ** best
    },
    addToDo(newToDo) {
      const { title, completed } = newToDo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(res => this.todos.push(res.data))
        .catch(err => console.log(err));

      //this.todo = [...this.todos, newToDo];
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(res => (this.todos = res.data))
      .catch(err => console.log(err));
  }
};
</script>
<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
