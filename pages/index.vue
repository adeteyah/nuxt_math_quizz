<script>
export default {
  data() {
    return {
      n1: 0,
      n2: 0,
      operator: "+",
      userInput: "",
    };
  },
  created() {
    this.nextQuestion();
    this.clearUserInput();
  },
  computed: {
    question() {
      return `${this.n1} ${this.operator} ${this.n2}`;
    },
  },
  methods: {
    clearUserInput() {
      this.userInput = "";
    },
    nextQuestion() {
      this.clearUserInput();
      this.n1 = this.getRandomNumber();
      this.n2 = this.getRandomNumber();
    },
    getRandomNumber() {
      return Math.floor(Math.random() * 10) + 1;
    },
    checkAnswer() {
      if (this.userInput == this.n1 + this.n2) {
        this.nextQuestion();
      }
    },
  },
};
</script>

<template>
  <div class="flex gap-2">
    <div>{{ question }}</div>
    <input
      class="w-[3ch]"
      type="text"
      v-model="userInput"
      v-on:keyup.enter="checkAnswer"
      autofocus
    />
  </div>
</template>
