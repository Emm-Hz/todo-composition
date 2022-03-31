<template>
  <i class="fa-solid fa-check checkMark" @click="close(task.id)"></i>
</template>

<script>
import { computed, inject } from "@vue/runtime-core";
export default {
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  setup() {
    const work = inject("todo");

    const close = (id) => {
      work.state = work.value.filter((item) => {
        if (item.id == id) {
          item.state = "done";
        }

        return item;
      });

      work.value = work.value.filter((item) => item.state != "done");

      console.log(work.state);
    };

    return { close };
  },
};
</script>

<style scoped>
.checkMark {
    padding: 0.5rem;
    border-radius: 50%;
    background-color: var(--background);
}
</style>