<script setup>
import { reactive, defineEmits } from 'vue';
import TodoButton from "../components/TodoButton.vue"

const emit = defineEmits(["create-todo"])

const todoState = reactive({
    todo: "",
    invalid: null,
    erMsg: ""
})

const createTodo = () => {
    todoState.invalid = null
    if (todoState.todo !== "") {
        emit("create-todo", todoState.todo);
        todoState.todo = "";
        return
    }
    todoState.invalid = true;
    todoState.erMsg = "Todo Value can't be empty"
}

</script>

<template>
    <div class="input-wrapper" :class="{ 'input-err': todoState.invalid }">
        <input type="text" v-model="todoState.todo" />
        <TodoButton @click="createTodo()" />
    </div>
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.erMsg }}</p>
</template>


<style lang="scss" scoped>
.input-wrapper {
    width: 100%;
    display: flex;
    justify-content: center;
    border: solid 3px transparent;
    transition: all;

    input {
        width: 100%;
        padding: 8px 6px;
        border: solid 1px rgba(0, 0, 0, 0.381);
        border-radius: 100px;

        &:focus {
            outline: solid 3px #41b0809c;
            box-shadow: 0 rgba(0, 0, 0, 0.247);
        }
    }
}

.err-msg {
    font-size: 13px;
    margin-top: 10px;
    color: red;
}
</style>