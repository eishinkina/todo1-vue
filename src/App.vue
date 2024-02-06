<template>
  <div>
    <h1>{{ title }} ✏️</h1>
    <div class="todo">
      <input type="text" v-model="todo" placeholder="Напишите дело..." />
      <button class="add-button" @click="addTodo">Добавить</button>

      <div v-for="(todo, i) in todos" :key="i">
        <p>
          <span class="todo__id">{{ i + 1 }}.</span>
          <span
            class="todo__text"
            :class="{ todo__text_isshow: todo.isDone }"
            >{{ todo.text }}</span
          >
          <input type="checkbox" v-model="todo.isDone" class="todo__check" />
          <button class="todo__btn" @click="removeTodo(i)">удалить</button>
        </p>
      </div>
      <hr />
      <p>Список задач: {{ todos.length }}</p>
    </div>
  </div>
</template>

<script>
export default {
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
      this.todos.push({ text: this.todo, isDone: false });
      this.todo = "";
    },
    removeTodo(i) {
      console.log(i);
      this.todos.splice(i, 1);
    },
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
