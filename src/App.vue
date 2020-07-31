<template>
  <div>
    <div class="container">
      <div>
        <h1 class="display-2 text-center">Vue Math Quiz</h1>
      </div>
      <hr>
      <div>
        <transition name="flip" mode="out-in">
          <component :is="selectedComponent"
                     @next="selectedComponent = 'app-question'"
                     @answered="answered($event)"></component>
        </transition>
      </div>
    </div>

  </div>
</template>

<script>
  import Question from "./components/Question.vue";
  import Answer from "./components/Answer.vue";

  export default {
    name: 'App',
    components: {
      appAnswer: Answer,
      appQuestion: Question
    },
    data() {
      return {
        selectedComponent: 'appQuestion',

      }
    },
    methods: {
      answered(isCorrect) {
        if (isCorrect){
          this.selectedComponent = 'app-answer'
        }else{
          this.selectedComponent = 'app-question'
          alert('WRONG!')
        }
      }
    }
  }
</script>

<style>
  .flip-enter{

  }
  .flip-enter-active{
    animation: flip-in 0.5s ease-out forwards;
  }
  .flip-leave{

  }
  .flip-leave-active{
    animation: flip-out 0.5s ease-out forwards;
  }
  @keyframes flip-in {
    from {
      transform: rotateY(90deg);
      filter: brightness(0.8);
    }
    to {
      transform: rotateY(0deg);
      filter: brightness(1);
    }
  }
  @keyframes flip-out {
    from {
      transform: rotateY(0deg);
      filter: brightness(1);
    }
    to {
      transform: rotateY(90deg);
      filter: brightness(0.8);
    }
  }

</style>
