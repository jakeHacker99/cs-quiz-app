<template>
  <div class="questionbox-container">
    <b-jumbotron lead="Bootstrap v4 Components for Vue.js 2">
      <template #lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />
      <b-list-group>
        <b-list-group-item  v-for="(answer, index) in answers" 
        :key="index"
        v-on:click="selectAnswer(index)"
        :class="[
        !answered && selectedIndex=== index ? 'selected': 
        answered && correctIndex === index ? 'correct' : 
        answered && selectedIndex === index && correctIndex !== index ?  'incorrect' : ''

        ]"
        >
          {{ answer }}</b-list-group-item
        >
      </b-list-group>

      <b-button variant="primary" 
      v-on:click="submitAnswer"
      :disabled="selectedIndex === null || answered"


      >Submit</b-button>
      <b-button v-on:click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  data() {
    return{
      selectedIndex:null,
      correctIndex:null,
      shuffledAnswers: [],
      answered: false
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    },
  },
  watch: {
    currentQuestion:{
      immediate:true,
      handler() {
        this.selectedIndex = null
        this.answered= false  
        this.shuffleAnswers()
      }
    }
    
    
    // () 
    // {
    //   this.selectedIndex=null
    //   this.shuffleAnswers()
    // }
  },
  methods:{
    selectAnswer(index) {
      this.selectedIndex=index
    },
    shuffleAnswers() {
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledAnswers= _.shuffle(answers)
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    },
    submitAnswer() {
      let isCorrect = false
      if (this.selectedIndex === this.correctIndex){
        isCorrect = true
      }
      this.answered = true

      this.increment(isCorrect)
    }
  },
  mounted() {
    this.shuffleAnswers()
  }
};
</script>


<style scoped>

.list-group{
  margin-bottom: 15px;
}

.list-group-item:hover{
  background: #eee;
  cursor: pointer;
}

.btn{
  margin: 0 5px;
}

.selected{
  background: royalblue;
}

.correct {
  background: limegreen;
}

.incorrect{
  background: red;
}
  

</style>