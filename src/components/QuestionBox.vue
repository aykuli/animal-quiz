<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>
        <div v-html="currentQuestion.question" />
      </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item
          v-for="(answer, i) in shuffledAnswers" 
          :key="answer"
          @click="selectAnswer(i)"
          :class="[answerClass(i)]"
          v-html="answer"
        />
      </b-list-group>


      <b-button 
        variant="primary"
        v-on:click="submitAnswer"
        :disabled="selectedIndex === null || answered"
      >
        Submit
        </b-button>
      <b-button 
        @click="next" 
        variant="success"
        :disabled="!answered"
      >
        Next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash';

export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function,
  },
  data: function () {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false
    }
  },
  computed: {
    answers() {
      const answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        this.shuffleAnswers();
      }
    },
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;
      this.increment(isCorrect);
    },
    shuffleAnswers() {
      const answersToShuffle= [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
      this.shuffledAnswers = _.shuffle(answersToShuffle);
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    },
    answerClass(i) {
      let answeredClass = '';
      if (!this.answered && this.selectedIndex === i) {
        answeredClass ='selected';
       } else if ( this.answered && this.correctIndex === i) {
         answeredClass = 'correct';
       } else if( this.answered 
                  && this.selectedIndex === i 
                  && this.correctIndex !== i) {
         answeredClass = 'incorrect';
       }
       return answeredClass;
    }
  },
}
</script>

<style scoped>
.list-group {
  margin-bottom: 30px;
}

.list-group-item:hover {
  background-color: #eeeeee;
  cursor: pointer;
}

.btn {
  margin: 0 5px;
}

.selected {
  background-color: #8db6d8;
}

.correct {
  background-color: #76d376;
}

.incorrect {
  background-color: #ff5252;
}
</style>