<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
  />
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  />
  <coppy-right-screen />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import CoppyRightScreen from "./components/CoppyRightScreen.vue";
import { shuffled } from "./utils/array";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    CoppyRightScreen,
  },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
        timer: null,
      },
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log(config);
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "match";
      console.log(this.statusMatch);
    },
    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;
      this.statusMatch = "result";
    },
  },
};
</script>

<style></style>
