<template>
  <div class="screen">
    <h1>Done</h1>
    <p>{{ Math.round(timer / 1000) }} seconds</p>
    <button @click="onStartAgain">Start Again</button>
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
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>
