<template>
  <div>
    <b-jumbotron header="Your result" lead="about knowing of animals">
      <p class="result">Correct answers: {{ numCorrect }}</p>
      <p class="result">Total number of questions: {{ numTotal }}</p>
      <b-button variant="primary" href="#">More Info</b-button>
    </b-jumbotron>
    {{ questions[0] }}
    <b-list-group>
      <b-list-group-item
        v-for="(question, i) in questions" 
        :key="question"
      >
        {{ i + 1 }}) {{ question.question }}
        <p class="answer">
          Answer: <span class="correct">{{ question.correct_answer }}</span>
          </p>
      </b-list-group-item>
    </b-list-group>
  </div>
</template>

<script>
export default {
  props: [
    'numCorrect', 'numTotal','questions'
  ]
}
</script>

<style scoped>
  .result {
    text-align: left;
  }

  .list-group {
    text-align: left;
  }

  .correct {
    padding: 5px 7px;

    background-color: #76d376;

    border-radius: 3px;
  }

  .answer {
    margin: 0;
  }

</style>