<template>
  <div>
    <h1>{{ title }} ✏️</h1>
    <div class="todo">
      <input type="text" v-model="todo" placeholder="Напишите дело..." />
      <button class="add-button" @click="addTodo">Добавить</button>
      <TodoList :todos="todos" @remove-todo="removeTodo" />
      <TodoTotal :todos="todos" />
      <hr />
    </div>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import TodoTotal from "./components/TodoTotal.vue";
export default {
  components: {
    TodoList,
    TodoTotal,
  },
  data() {
    return {
      title: "Список дел...",
      todo: "",
      todos: [],
      isDone: false,
    };
  },
  methods: {
    addTodo() {
      if (!this.todo) return alert("Введите дело");
      this.todos.push({ text: this.todo, isDone: false });
      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.todo = "";
    },
    removeTodo(i) {
      console.log(i);
      this.todos.splice(i, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
  mounted() {
    const data = localStorage.getItem("todos");
    data && (this.todos = JSON.parse(data));
  },
};
</script>

<style lang="scss">
h1 {
  text-align: center;
}

.todo {
  width: 300px;
  background-color: rgb(243, 227, 247);
  padding: 30px;
  outline: 1px solid #000;
  min-height: 500px;
  margin: 0 auto;

  &__id {
    color: red;
    font-weight: bold;
  }

  &__text {
    font-size: 15px;
    color: rgb(81, 82, 82);
    text-transform: capitalize;
    position: relative;

    &_isshow::after {
      content: "";
      position: absolute;
      left: 0;
      right: 0;
      top: 50%;
      border-top: 1px solid rgb(240, 4, 55);
    }
  }

  &__check {
    margin-left: 30px;
    display: inline-block;
  }
  &__btn {
    padding: 5px 10px;
    background-color: #ff4d4d;
    border: none;
    border-radius: 4px;
    color: white;
    font-weight: bold;
    cursor: pointer;
    transition: background-color 0.3s;
    &:hover {
      background-color: #ff1a1a;
    }
  }
}
.add-button {
  padding: 5px 10px;
  background-color: #ff4d4d;
  border: none;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s;
  margin-left: 10px;
}

.add-button:hover {
  background-color: #cc0000;
}
</style>
