<template>
  <div class="todo-input">
    <input
      v-model="newTodo"
      placeholder="할일을 입력하세요"
      @keyup.enter="submitTodo"
    />
    <button @click="submitTodo">추가</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: "",
    };
  },
  methods: {
    // 이벤트 처리 함수 선언
    submitTodo() {
      if (this.newTodo.trim() === "") {
        alert("내용을 입력해주세요!");
        return;
      } else {
        this.$emit("addTodo", this.newTodo);
        // 상위 컴포넌트인 APP의 addTodo 메서드의 인수로 newTodo 전달하며 호출
        this.newTodo = "";
      }
    },
  },
};
</script>
