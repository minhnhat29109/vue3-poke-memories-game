<template>
  <div class="screen">
    <h1>Done</h1>
    <p>{{ Math.round(timer / 1000) }} seconds</p>
    <button>Start Again</button>
  </div>
</template>
<script>
export default {
  props: {
    timer: {
      type: Number,
      require: true,
    },
  },
};
</script>
