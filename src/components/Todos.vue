<template>
  <div>
    <!-- loop through the array passed from the app component -->
    <div v-bind:key="todo.id" v-for="todo in todos">
      <!-- write out the TodoItem tag and send  data (todo object) to the TodoItem component -->
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
    </div>
  </div>
</template>
<script>
// import the TodoItem component
import TodoItem from "./TodoItem.vue";
export default {
  name: "Todos",
  components: {
    // define the TodoItem component here
    TodoItem
  },
  // return the props back to the app component as an array
  props: ["todos"]
};
</script>
<style scoped>
</style>
