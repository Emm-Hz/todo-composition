<template>
  <div class="page">
    <h1>TODO LIST</h1>
    <Todo />
  </div>
</template>

<script setup>
import Todo from "@/components/Todo.vue";
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Fira+Sans:wght@700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@500&display=swap');

:root {
  /* Colors */
  --background: #2a2d43;
  --task: #414361;
  --button: #7f2ccb;
  --disable: #8d99ae;
  --white: #ffffff;

  /* Fonts */
  --fira: 'Fira Sans', sans-serif;
  --quick: 'Quicksand', sans-serif;
}

body {
  background: var(--background);
}

h1 {
  margin-bottom: 5rem;
  font-family: var(--fira);
  font-size: 4em;
  line-height: 1rem;
  text-decoration: underline;
  color: var(--white);
}

.page {
  display: flex;
  flex-direction: column;
  place-content: center;
  place-items: center;
  min-height: 98vh;
}
</style>
