<template>
  <h1>Interact component</h1>
  <card-flip
    v-for="(card, index) in cardsContext"
    :key="index"
    :ref="`card-${index}`"
    :imgBackFaceUrl="`images/${card}.png`"
    :card="{ index, value: card }"
    @onFlip="checkRule($event)"
  />
</template>
<script>
import CardFlip from "./Card.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
  data() {
    return {
      rules: [],
      count: 0,
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;

      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value == this.rules[1].value
      ) {
        console.log("Right...");
        this.$refs[`card-${this.rules[0].index}`][0].onDisableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onDisableMode();
        this.rules = [];
        this.count++;
        if (this.count === this.cardsContext.length / 2) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
</script>
