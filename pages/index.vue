<template>
    <div>
      <h1>TODOリスト</h1>
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" placeholder="新しいタスクを追加">
        <button type="submit">追加</button>
      </form>
      <ul>
        <li v-for="(todo, index) in todoStore.todos" :key="index">
          {{ todo }}
          <button @click="removeTodo(index)">削除</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { useTodoStore } from '~/src/stores/todo';
  
  const newTodo = ref('');
  const todoStore = useTodoStore();
  
  const addTodo = () => {
    if (newTodo.value.trim() !== '') {
      todoStore.addTodo(newTodo.value);
      newTodo.value = '';
    }
  };
  
  const removeTodo = (index) => {
    todoStore.removeTodo(index);
  };
  </script>
  