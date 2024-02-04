<script setup>
import { Icon } from "@iconify/vue";
import { defineProps, defineEmits, ref, reactive } from "vue";
const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  },
});
const todoValue = reactive({
  value: "",
});

const emit = defineEmits([
  "toggle-complete",
  "edit-todo",
  "update-todo",
  "delete-todo",
]);

const handleEditTextarea = (ev, index, todo) => {
  if (todoValue.value === "") {
    todoValue.value = todo.trim();
  }

  const value = ev.target.value;
  todoValue.value = value.trim();
  emit("update-todo", value, index);
};
</script>

<template>
  <li>
    <input
      type="checkbox"
      :checked="todo.isCompleted"
      @input="$emit('toggle-complete', index)"
    />
    <div class="todo">
      <textarea
        v-if="todo.isEditing"
        :value="todo.todo"
        @input="(ev) => handleEditTextarea(ev, index, props.todo.todo)"
      ></textarea>
      <span v-else :class="{ 'completed-todo': todo.isCompleted }">
        {{ todo.todo }}
      </span>
    </div>
    <div class="todo-actions">
      <Icon
        v-if="todo.isEditing"
        icon="ph:check-circle"
        width="22"
        height="22"
        class="icon"
        style="color: #41b008"
        @click="$emit('edit-todo', todoValue.value, index)"
      />
      <Icon
        v-else
        icon="ph:pencil-fill"
        width="22"
        height="22"
        class="icon"
        style="color: #41b008"
        @click="$emit('edit-todo', 'edit', index)"
      />
      <Icon
        icon="ph:trash"
        width="22"
        height="22"
        class="icon"
        style="color: #f95e5e"
        @click="$emit('delete-todo', todo.id)"
      />
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 16px 10px;
  background-color: #f1f1f1;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);

  &:hover {
    .todo-actions {
      opacity: 1;
    }
  }

  input[type="checkbox"] {
    appearance: none;
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50%;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);

    &:checked {
      background-color: #41b080;
    }
  }

  .todo {
    flex: 1;
    width: auto;
    height: auto;
    overflow: hidden; /* إضافة خاصية overflow للتحكم في النصوص الطويلة */
    white-space: wrap; /* تجنب السماح بالفواصل الأوتوماتيكية في النصوص */
    text-overflow: ellipsis; /* إظهار نقاط تعليق (...) عند تجاوز النص عرض العنصر */

    .completed-todo {
      text-decoration: line-through;
    }

    textarea {
      width: 100%;
      padding: 2px 6px;
      border: 2px solid #41b080;
      resize: vertical; /* تمكين إعادة التحجيم الرأسي لمربع النص */
    }
  }

  .todo-actions {
    display: flex;
    gap: 6px;
    opacity: 0;
    transition: 150ms ease-in-out;
    .icon {
      cursor: pointer;
    }
  }
}
</style>
