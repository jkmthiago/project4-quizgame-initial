<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div>
    <h1 v-html="this.question">
    </h1>

    <template>
      <label>True</label>
      <input type="radio" name="options" value="True"><br>
    </template>

    <button class="send" type="button">Send</button>

  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswer: undefined,
    }
  },

  computed: {
    answers(){
      var answers = [...this.incorrectAnswers];
      answers.splice(Math.round(Math.random()*answers.length), 0, this.correctAnswer)
      return answers;
    }
  },

  created() {
    this.axios.get('https://opentdb.com/api.php?amount=10&category=18&difficulty=hard&type=multiple').then((response) => {
      this.question = response.data.results[0].question;
      this.incorrectAnswers = response.data.results[0].incorrect_answers;
      this.correctAnswer = response.data.results[0].correct_answer;
      
    })
  },
  components: {
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 960px;

  input {
    margin: 12px 4px;
  }

  button.send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #ffffff;
    background-color: #1867c0;
    border: 1px solid #1867c0;
    border-radius: 30px;
    cursor: pointer;
    transition: .4s;
  }

  button.send:hover {
    border: 5px solid #1867c0;
    background-color: #0b396d;
  }
}
</style>
