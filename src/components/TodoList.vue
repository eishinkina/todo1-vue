<template>
  <div>
    <div v-for="(todo, i) in todos" :key="i">
      <p>
        <span class="todo__id">{{ i + 1 }}.</span>
        <span class="todo__text" :class="{ todo__text_isshow: todo.isDone }">{{
          todo.text
        }}</span>
        <input type="checkbox" v-model="todo.isDone" class="todo__check" />
        <button class="todo__btn" @click="removeTodo(i)">удалить</button>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: [Array, Object],
      required: true,
    },
  },
  methods: {
    removeTodo(i) {
      this.$emit("remove-todo", i);
    },
  },
};
</script>

<style lang="scss" scoped></style>
