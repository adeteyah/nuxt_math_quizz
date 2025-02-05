<script>
export default {
  data() {
    return {
      min: 1,
      max: 9,
      n1: 0,
      n2: 0,
      operators: ["+", "-", "*"],
      operator: null,
      userInput: "",
    };
  },
  created() {
    this.nextQuestion();
    this.getRandomOperator();
    this.clearUserInput();
  },
  computed: {
    question() {
      return `${this.n1} ${this.operator} ${this.n2}`;
    },
  },
  methods: {
    getRandomOperator() {
      this.operator =
        this.operators[Math.floor(Math.random() * this.operators.length)];
    },
    clearUserInput() {
      this.userInput = "";
    },
    nextQuestion() {
      this.clearUserInput();
      this.getRandomOperator();
      this.n1 = this.getRandomNumber(this.min, this.max);
      this.n2 = this.getRandomNumber(this.min, this.max);
    },
    getRandomNumber(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    checkAnswer() {
      switch (this.operator) {
        case "+":
          if (this.userInput == this.n1 + this.n2) {
            this.nextQuestion();
          }
          break;
        case "-":
          if (this.userInput == this.n1 - this.n2) {
            this.nextQuestion();
          }
          break;
        case "*":
          if (this.userInput == this.n1 * this.n2) {
            this.nextQuestion();
          }
          break;

        default:
          break;
      }
    },
  },
};
</script>

<template>
  <div class="h-svh flex justify-center items-center gap-4">
    <span class="text-5xl">{{ question }} = </span>
    <input
      class="w-[2.4ch] text-center text-5xl rounded"
      type="text"
      v-model="userInput"
      v-on:keyup.enter="checkAnswer"
      autofocus
    />
  </div>
</template>
