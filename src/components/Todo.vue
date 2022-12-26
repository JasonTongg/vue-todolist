<template>
  <div class="Container">
    <div class="TodoContainer" :key="index" v-for="(item, index) in todo">
      <input type="checkbox" :id="index" @click="setData(index)" />
      <label :for="index" :class="item.status ? 'active' : null">
        {{ item.text }}
      </label>
    </div>
  </div>
</template>
<script>
export default {
  name: 'TodoVue',
  props: {
    todo: {
      type: Number,
      default: [],
    },
    setData: {
      type: Function,
      required: true,
    },
  },
};
</script>
<style scoped>
.Container {
  display: flex;
  width: 100%;
  align-items: flex-start;
  justify-content: center;
  flex-direction: column;
  gap: 1rem;
  padding: 1rem;
}
.TodoContainer {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  gap: 0.5rem;
}

.TodoContainer label {
  color: var(--primaryColor);
  font-weight: bolder;
  font-size: 1.1rem;
  text-transform: capitalize;
}

.TodoContainer label.active {
  text-decoration: line-through;
}
</style>
