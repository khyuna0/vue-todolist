<template>
  <div id="app">
    <h1>Todo List</h1>
    <TodoInput @addTodo="add_Todo" />
    <TodoList :todos="todos" @deleteTodo="todoDelete" />
  </div>
</template>

<script>
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import api from "./config/axiosConfig";

export default {
  name: "App",
  components: {
    TodoInput,
    TodoList,
  },

  data() {
    return {
      todos: [],
      // nextId: 1,
    };
  },

  async created() {
    // 페이지 로딩 시에 자동으로 호출 (useEffect)
    await this.loadTodos(); // 페이지가 로딩될 때 새로운 벡엔드 할일 목록 불러오기
  },

  methods: {
    async loadTodos() {
      // 기존 할일 리스트 가져오기
      try {
        const res = await api.get("/todos"); // 모든 할일 리스트 가져오기 호출
        this.todos = res.data;
      } catch (err) {
        console.error("TodoList 불러오기 실패", err);
      }
    },

    async add_Todo(newTodoText) {
      try {
        const res = await api.post("/todos", { content: newTodoText });
        this.todos.push(res.data);
      } catch (err) {
        console.error("할일 추가 실패", err);
      }
    },

    //   this.todos.push({
    //   id: Date.now(), // 현재시간(밀리터리 초 단위) -> 절대 중복되지 않는 값
    //   content: newTodoText,
    // });

    todoDelete(id) {
      // id-> TodoList에서 넘어온 todo.id (삭제할 할일의 id)
      this.todos = this.todos.filter((todo) => todo.id !== id);
      // 조건에 맞지 않는 요소들만 남김
    },
  },
};
</script>

<style>
#app {
  max-width: 400px;
  text-align: center;
  margin: 50px auto;
  border: 1px solid #eee;
  border-radius: 10px;
  background-color: #faf9f9;
  padding: 10px;
}

#app h1 {
  color: cadetblue;
}
</style>
