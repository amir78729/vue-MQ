<template>
  <div class="panel panel-default">
    <div class="panel-heading">
      <h3 class="panel-title display-3 text-center">{{ question }}</h3>
    </div>
    <div class="panel-body">
      <div class="col-xs-12 col-sm-6 col-lg-3 text-center">
        <button class="answer-btn btn btn-dark btn-lg" @click="onAnswer(btnData[0].correct)">{{ btnData[0].answer }}</button>
      </div>
      <div class="col-xs-12 col-sm-6 col-lg-3 text-center">
        <button class="answer-btn btn btn-dark btn-lg" @click="onAnswer(btnData[1].correct)">{{ btnData[1].answer }}</button>
      </div>
      <div class="col-xs-12 col-sm-6 col-lg-3 text-center">
        <button class="answer-btn btn btn-dark btn-lg" @click="onAnswer(btnData[2].correct)">{{ btnData[2].answer }}</button>
      </div>
      <div class="col-xs-12 col-sm-6 col-lg-3 text-center">
        <button class="answer-btn btn btn-dark btn-lg" @click="onAnswer(btnData[3].correct)">{{ btnData[3].answer }}</button>
      </div>
    </div>
  </div>
</template>
<script>
  const MODE_ADD = 1;
  const MODE_SUB = 2;
  export default {
    data() {
      return {
        question: 'No Question in Entered!',
        btnData: [
          {correct: true, answer: 0},
          {correct: false, answer: 0},
          {correct: false, answer: 0},
          {correct: false, answer: 0}
        ]
      };
    },
    methods: {
      generateQuestion(){
        const num1 = this.generateRandomNumber(1,100);
        const num2 = this.generateRandomNumber(1,100);
        const mode = this.generateRandomNumber(1,2);

        let correctAnswer = 0;
        switch (mode) {
          case (MODE_ADD):
            correctAnswer = num1 + num2;
            this.question = 'What is ' + num1 + ' + ' + num2 + '?';
            break;
          case (MODE_SUB):
            correctAnswer = num1 - num2;
            this.question = 'What is ' + num1 + ' - ' + num2 + '?';
            break;
          default:
            correctAnswer = 0;
            this.question = 'oops';
        }
        this.btnData[0].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
        this.btnData[1].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
        this.btnData[2].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
        this.btnData[3].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
        this.btnData[0].correct = false;
        this.btnData[1].correct = false;
        this.btnData[2].correct = false;
        this.btnData[3].correct = false;

        const correctButton = this.generateRandomNumber(0,3);
        this.btnData[correctButton].answer = correctAnswer;
        this.btnData[correctButton].correct = true;
      },
      generateRandomNumber(min, max , except) {
        const rand = Math.round(Math.random() * (max - min) + min);
        if (rand == except){
          return this.generateRandomNumber(min, max , except);
        }
        return rand
      },
      onAnswer(inCorrect){
        this.$emit('answered', inCorrect);
      }
    },
    created(){
      this.generateQuestion();
    }
  }
</script>
<style>
  .answer-btn {
    margin: 20px;
    width: 90px;
  }
</style>