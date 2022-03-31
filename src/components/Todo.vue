<template>
  <div class="wrapp">
    <form class="taskForm" @submit.prevent="task">
      <input
        class="taskInput"
        type="text"
        placeholder="Add your task"
        v-model.trim="text"
      />
      <button
        class="btnDisable"
        :class="{ taskButton: text != '' ? true : false }"
        :disabled="text == '' ? true : false"
      >
        Add Task
      </button>
    </form>

    <div class="taskList" v-for="item in homeworks" :key="item.id">
      <p class="taskLetter">{{ item.task }}</p>
      <buttons :task="item" />
    </div>
  </div>
</template>

<script>
import { computed, provide, ref, watchEffect } from "vue";
import Buttons from "./Buttons.vue";

let id = 0;

export default {
  components: { Buttons },
  setup() {
    const text = ref("");
    const homeworks = ref([]);

    provide("todo", homeworks);

    if (localStorage.getItem("taskList")) {
      homeworks.value = JSON.parse(localStorage.getItem("taskList"));
    }

    const task = () => {
      const taskArray = {
        task: text.value,
        id: Date.now(),
        state: "progress",
      };

      homeworks.value.push(taskArray);

      text.value = "";
    };

    watchEffect(() => {
      localStorage.setItem("taskList", JSON.stringify(homeworks.value));
    });

    return { text, task, homeworks };
  },
};
</script>

<style scoped>
.wrapp {
  display: flex;
  flex-direction: column;
  min-width: 46vw;
}

.taskForm {
  display: flex;
  place-items: center;
  justify-content: space-around;
  margin-bottom: 2rem;
  width: 100%;
}

.taskInput {
  margin-right: .5rem;
  width: 100%;
  height: 2.5rem;
  border: none;
  border-radius: 5px;
  outline: none;
}

.btnDisable {
  width: 30%;
  height: 2.5rem;
  border: none;
  border-radius: 5px;
  color: white;
  background-color: var(--disable);
}
.taskButton {
  width: 30%;
  height: 2.5rem;
  border: none;
  border-radius: 5px;
  color: white;
  background-color: var(--button);
}

.taskList {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  margin-bottom: .2rem;
  padding: 1rem;
  width: 95%;
  border-radius: 5px;
  font-family: var(--quick);
  color: white;
  background: var(--task);
}

.taskLetter {
  margin: 0;
}
</style>