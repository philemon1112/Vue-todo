<script setup>
  import TodoCreatorVue from '../components/TodoCreator.vue';
  import TodoItem from '../components/TodoItem.vue';
  import { Icon } from "@iconify/vue";
  import {uid} from 'uid';
  import {ref} from "vue"

  const todoLists = ref([]);

  const createTodo = (todo) => {
    todoLists.value.push({
      id: uid(),
      todo,
      isCompleted: null,
      isEditing: null
    })
  }

const toggleTodoComplete = (todoPos)=> {
  todoLists.value[todoPos].isCompleted = !todoLists.value[todoPos].isCompleted
}
const toggleEditTodo = (todoPos)=> {
  todoLists.value[todoPos].isEditing = !todoLists.value[todoPos].isEditing
}


</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreatorVue @create-todo="createTodo" />
    <ul v-if="todoLists.length > 0">
      <TodoItem 
        v-for="(todo, index) in todoLists" 
        :key="todo.id" 
        :todo="todo" 
        :index="index"  
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
      />
    </ul>
    <p class="todo-msg" v-else>
      <Icon icon="noto-v1:sad-but-relieved-face" width="22" />
      <span> You have no todo's to complete! Add One</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
}
</style>
