<script setup>
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";
import { Icon } from "@iconify/vue";
import { ref, watch, computed } from "vue";
import { uid } from "uid";

const todoList = ref([]);

watch(
  todoList,
  () => {
    setTodoListLocalStorage();
  },
  {
    deep: true,
  }
);

const todoCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("todoList"));

  if (savedTodoList) {
    todoList.value = savedTodoList;
  }
};

fetchTodoList();

const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};

const toogleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
};

const toogleEditTodo = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
};

const onUpdateTodo = (todoVal, todoPos) => {
  todoList.value[todoPos].todo = todoVal;
};

const toogleDeleteTodo = (todoIndex) => {
  todoList.value = todoList.value.filter((val) => val.id !== todoIndex);
};
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul>
      <TodoItem
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        @toggle-complete="toogleTodoComplete"
        @edit-todo="toogleEditTodo"
        @update-todo="onUpdateTodo"
        @delete-todo="toogleDeleteTodo"
      />
    </ul>
    <p v-if="todoList.length == 0" class="todos-msg">
      <Icon icon="fe:cry" width="30" />
      <span>You haven't todo's to complete! Add one!</span>
    </p>
    <p v-if="todoCompleted && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper" />
      <span>You have complete all your todos!</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 500px;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  ul {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-top: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-top: 10px;
  }
}
</style>
