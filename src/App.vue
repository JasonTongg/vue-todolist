<template>
  <div class="overlay">
    <div class="container">
      <h1>TODOLIST</h1>
      <form class="InputContainer" @submit.prevent="addTodo($event)">
        <input type="text" placeholder="Add todo..." />
        <button type="submit">+</button>
      </form>
      <List :todo="todo" :setData="setData" />
      <div class="info">
        <p>
          {{ todo.filter((item) => item.status === true).length }} of
          {{ todo.length }} tasks done
        </p>
        <button @click="RemoveChecked">Remove Checked</button>
      </div>
    </div>
  </div>
</template>
<script>
import List from './components/Todo.vue';
export default {
  name: 'TodoVue',
  data() {
    return {
      todo: [
        {id: 1, text: 'jason', status: false},
        {id: 2, text: 'toni', status: false},
      ],
    };
  },
  methods: {
    setData(index) {
      let todoList = [...this.todo];
      todoList[index].status = !todoList[index].status;
      this.todo = todoList;
    },
    addTodo(event) {
      if (!event.target.querySelector('input').value) return;
      this.todo = [
        ...this.todo,
        {
          id: +new Date(),
          text: event.target.querySelector('input').value,
          status: false,
        },
      ];
    },
    RemoveChecked() {
      this.todo = this.todo.filter((item) => item.status === false);
    },
  },
  components: {
    List,
  },
};
</script>
<style scoped>
.overlay {
  background-color: var(--primaryColor);
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.container {
  padding: 1rem 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 500px;
  height: fit-content;
  background-color: white;
}
.InputContainer {
  width: 100%;
  display: grid;
  grid-template-columns: auto 50px;
  gap: 0.5rem;
  margin-top: 1rem;
}
.InputContainer input {
  text-align: center;
  border: 1px solid var(--primaryColor);
  outline: none;
  padding: 0.5rem 1rem;
  font-size: 1.2rem;
}
.InputContainer button {
  height: 100%;
  font-size: 2rem;
  color: white;
  background-color: var(--primaryColor);
  border: none;
  outline: none;
  cursor: pointer;
}
.info {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  width: 100%;
}

.info p {
  text-align: center;
  width: 100%;
}

.info button {
  background-color: var(--primaryColor);
  color: white;
  border: none;
  outline: none;
  padding: 0.3rem 0.5rem;
  cursor: pointer;
  width: 100%;
}
</style>
