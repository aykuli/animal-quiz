<template>
  <div id="app">
    <Header 
      :numCorrect="numCorrectAnswers"
      :numTotal="numTotal"
    />

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length > 0"
            :currentQuestion="questions[index]" 
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <Result 
            :numCorrect="numCorrectAnswers"
            :numTotal="numTotal"
            :questions="questions"
          />
        </b-col>
      </b-row>
    </b-container>
    

  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import Result from './components/Result.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Result
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrectAnswers: 0,
      numTotal: 0,
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrectAnswers++;
      }
      this.numTotal++;
    }
  },
  mounted: function () {
    const url = 'https://opentdb.com/api.php?amount=10&category=27&type=multiple'
    fetch(url, {method: 'get'})
    .then(res=>res.json()).then(data=> {
      this.questions = data.results;
    });
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
