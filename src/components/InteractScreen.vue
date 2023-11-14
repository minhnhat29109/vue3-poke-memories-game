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
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
        this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
        this.rules = [];
      } else return false;
    },
  },
};
</script>
