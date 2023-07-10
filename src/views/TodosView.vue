<script setup>
import TodoCreator from '../components/TodoCreator.vue';
import TodoItem from '../components/TodoItem.vue';
import { Icon } from '@iconify/vue';
import { ref } from "vue"
import { uid } from "uid"

const todoList = ref([])

const createTodo = (todo) => {
    todoList.value.push({
        id: uid(),
        todo,
        isCompleted: null,
        isEditing: null
    })
}

const toogleTodoComplete = (todoPos) => {
    todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted
}
</script>

<template>
    <main>
        <h1>Create Todo</h1>
        <TodoCreator @create-todo="createTodo" />
        <ul>
            <TodoItem v-for="(todo, index) in todoList" :todo="todo" :index="index" @toggle-complete="toogleTodoComplete" />
        </ul>
        <p v-if="!todoList" class="todos-msg">
            <Icon icon="fe:cry" width="30" />
            <span>You haven't todo's to complete! Add one!</span>
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
    }
}
</style>
