<template>
    <div class="question-box-container">
      <b-jumbotron>
        <template #lead>
          {{ currentQuestion.question }}
        </template>

        <hr class="my-4">

        <b-list-group>
          <b-list-group-item
              v-for="(answer, index) in answers"
              :key="index"
              @click="selectAnswer(index)"
              :class="[selectedIndex === index ? 'selected' : '']"
          >
            {{answer}}
          </b-list-group-item>
        </b-list-group>

        <b-button variant="primary" href="#">Submit</b-button>
        <b-button @click="next" variant="success" href="#">Next question</b-button>
      </b-jumbotron>
    </div>
</template>

<script>
export default {
  name: "QuestionBox",
  props: {
    currentQuestion: Object,
    next: Function
  },
  data() {
    return {
      selectedIndex: null
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  watch: {
    currentQuestion() {
      this.selectedIndex = null
      this.shuffleAnswers()
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    shuffleAnswers() {
      //let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
    }
  },
  mounted() {
    console.log(this.currentQuestion)
  }
}
</script>

<style scoped>

  .list-group {
    margin-bottom: 15px;
  }
  .selected {
    background-color: lightblue;
  }
  .correct {
    background-color: lightgreen;
  }
  .incorrect {
    background-color: lightcoral;
  }
  .list-group-item:hover {
    background-color: #EEE;
    cursor: pointer;
  }
  .btn {
    margin: 0 5px;
  }

</style>

