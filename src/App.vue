<template>
  <div id="app">
    <Header 
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    
    />

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <Questionbox 
          v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header";
import Questionbox from "./components/Questionbox";

export default {
  name: "App",
  components: {
    Header,
    Questionbox,
  },
  data() {
    return{
      questions:[],
      index:0,
      numCorrect: 0,
      numTotal:0
    }
  },
  methods:{
    next() {
      this.index++
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++
      }
      this.numTotal++
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=18&difficulty=easy&type=multiple',{
      method:'get'
    })
      .then((response) =>{
        return(response.json());
      })
      .then((jsonData) =>{
        this.questions= jsonData.results
      })
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-image: linear-gradient(#4B0082, #9370DB, 	#9400D3);
}
html{
  background: url(./assets/cs5-bg.jpg);
}

</style>
