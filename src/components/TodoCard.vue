<template>
  <li class="TodoCard">
    <span>
      <input type="checkbox" class="checkbox" :value="done" @click="toggleTodo" :checked="done" />
    </span>
    <span :class="{ done: done }" class="title">{{ todo.title }}</span>
    <span v-if="done" @click="deleteTodo()" class="material-icons desc">close</span>
  </li>
</template>

<script>
import { computed } from "vue";
export default {
  name: "TodoCard",
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  setup(props, context) {
    const done = computed(() => props.todo.done);
    return {
      done,
      toggleTodo: () => {
        const value = {
          ...props.todo,
          done: !props.todo.done,
        };
        context.emit("change", value);
      },
      deleteTodo: () => {
        context.emit("delete", props.todo.id);
      },
    };
  },
};
</script>
