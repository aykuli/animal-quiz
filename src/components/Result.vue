<template>
  <div>
    <b-jumbotron header="Your result" lead="about knowing of animals">
      <p class="result">Correct answers: {{ numCorrect }}</p>
      <p class="result">Total number of questions: {{ numTotal }}</p>
      <b-button
        variant="primary"
        v-on:click="startAgain"
      >
        Start again
      </b-button>

      <b-list-group>
        <b-list-group-item
          v-for="(question, i) in questions" 
          :key="question + i"
        >
          <div class="question">
            {{ i + 1 }}) {{ question.question }}
          </div>
          <div class='property'>
            <span class="property">Answer: </span>
            <span class="value-answer">{{ question.correct_answer }}</span>
          </div>
          <div class='property'>
            <span class="property">Difficulty: </span>
            <span class="value">{{ question.difficulty }}</span>
          </div>          
        </b-list-group-item>
      </b-list-group>

      <b-button 
        variant="primary" 
        @click="startAgain"
      >
        Start again
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  props: [
    'numCorrect', 'numTotal','questions', 'startAgain'
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

  .value-answer {
    padding: 5px 7px;
    margin-bottom: 15px;

    background-color: #76d376;

    border-radius: 3px;
  }

  .property, .question {
    margin: 15px 0;
  }

  .value {
    margin-bottom: 15px;
  }

  .btn {
    margin: 15px 0;
  }

</style>