<template>
  <div>
    <p>Список задач: {{ todos.length }}</p>
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
};
</script>

<style lang="scss" scoped></style>
