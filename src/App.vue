<template>
  <div id="app">
    <div v-if="gameEnded">
      <h1>Oops! Se nos acabaron las preguntas...</h1>
      <a
        href="https://github.com/brunogonzales/namesgame"
      >Envia tus preguntas al repositorio en GitHub</a>
    </div>
    <div v-else>
      <button @click="nextSlide">Siguiente</button>
      <h2>{{currentPlayer}}</h2>
      <h4>{{currentQuestion}}</h4>
    </div>
  </div>
</template>

<script>
import { questions } from "./constants";

export default {
  name: "App",
  data() {
    return {
      players: [],
      currentPlayer: "",
      currentQuestion: "",
      questions
    };
  },
  created() {
    this.setPlayers();
    this.nextSlide();
  },
  methods: {
    setPlayers() {
      this.players = prompt(
        "Ingresa los nombres de los players separados por una coma"
      ).split(",");
    },

    nextSlide() {
      if (!this.questions.length) {
        this.gameEnded = true;
      } else {
        const randomQuestionIndex = this.randomNumber(this.questions.length);
        this.currentPlayer = this.players[
          this.randomNumber(this.players.length)
        ];
        this.currentQuestion = this.questions[randomQuestionIndex];
        this.questions = [
          ...this.questions.slice(0, randomQuestionIndex),
          ...this.questions.slice(randomQuestionIndex + 1)
        ];
      }
    },

    randomNumber(max) {
      return Math.floor(Math.random() * max);
    }
  }
};
</script>

<style>
#app {
  padding: 15px;
}
</style>
