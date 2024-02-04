<script setup>
import { ref, watch, computed, reactive } from "vue";
import { uid } from "uid";
import TodoCreator from "@/components/TodoCreator.vue";
import TodoItem from "@/components/TodoItem.vue";
import { Icon } from "@iconify/vue";
const todoList = ref([]);
const todoStateInUpdate = reactive({
  invalid: null,
  errMsg: "",
});
watch(
  todoList,
  () => {
    setTodoListLocalStorage();
  },
  { deep: true }
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
  todoList.value.unshift({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};

const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
};

const toggleEditTodo = (todoVal, todoPos) => {
  todoStateInUpdate.invalid = null;
  if (todoVal === "edit") {
    todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
  } else if (todoVal === "") {
    todoStateInUpdate.invalid = true;
    todoStateInUpdate.errMsg = "Todo value cannot be empty in update";
  } else {
    todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
  }
};

const updateTodo = (todoVal, todoPos) => {
  todoList.value[todoPos].todo = todoVal;
};

const deleteTodo = (todoId) => {
  todoStateInUpdate.invalid = null;
  const updatedTodo = todoList.value.filter((todo) => todo.id !== todoId);
  todoList.value = updatedTodo;
};
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo" />
    <p v-if="todoCompleted && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper" />
      <span>You have completed all your todos!</span>
    </p>
    <p v-show="todoStateInUpdate.invalid" class="err-msg">
      {{ todoStateInUpdate.errMsg }}
    </p>
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
      />
    </ul>
    <p v-else class="todos-msg">
      <Icon icon="noto-v1:sad-but-relieved-face" width="22" />
      <span>You have no todo's to complete Add one!</span>
    </p>
  </main>
</template>

<style scoped lang="scss">
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
  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
  .err-msg {
    margin-top: 6px;
    font-size: 12px;
    text-align: center;
    color: red;
  }
}
</style>
