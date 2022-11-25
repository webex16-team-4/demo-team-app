<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. {{ quizzes[qNum].text }}</h2>
    <img
      class="quiz-image"
      src="https://via.placeholder.com/300x300"
      alt="クイズタイトル"
    />
    <div class="container">
      <button v-on:click="choose1">
        {{ quizzes[qNum].choices[0].text }}
      </button>
      <button v-on:click="choose2">
        {{ quizzes[qNum].choices[1].text }}
      </button>
      <button v-on:click="choose3">
        {{ quizzes[qNum].choices[2].text }}
      </button>
    </div>
    <div v-if="answer == 1">
      <div v-if="quizzes[qNum].choices[0].isCorrect == 1">正解！</div>
      <div v-if="quizzes[qNum].choices[0].isCorrect == 0">不正解！</div>
      <div>{{ quizzes[qNum].choices[0].feedback }}</div>
    </div>
    <div v-if="answer == 2">
      <div v-if="quizzes[qNum].choices[1].isCorrect == 1">正解！</div>
      <div v-if="quizzes[qNum].choices[1].isCorrect == 0">不正解！</div>
      <div>{{ quizzes[qNum].choices[1].feedback }}</div>
    </div>
    <div v-if="answer == 3">
      <div v-if="quizzes[qNum].choices[2].isCorrect == 1">正解！</div>
      <div v-if="quizzes[qNum].choices[2].isCorrect == 0">不正解！</div>
      <div>{{ quizzes[qNum].choices[2].feedback }}</div>
    </div>

    <div v-if="nextQuiz">
      <p></p>
      <button v-on:click="nextQ">次の問題へ</button>
    </div>
    <div>{{ qNum }}</div>

    <!-- <div>{{ "答え" }}</div> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      qNum: 0,
      answer: 0,
      nextQuiz: false,
      quizzes: [
        //1問目
        {
          text: "1問目",
          // image:
          choices: [
            {
              text: "1",
              isCorrect: 1,
              feedback: "1feed",
            },
            {
              text: "2",
              isCorrect: 0,
              feedback: "2feed",
            },
            {
              text: "3",
              isCorrect: 0,
              feedback: "3feed",
            },
          ],
        },
      ],
    }
  },
  methods: {
    choose1: function () {
      this.answer = 1
      if (this.quizzes[this.qNum].choices[0].isCorrect == 1) {
        this.nextQuiz = true
      }
    },
    choose2: function () {
      this.answer = 2
      if (this.quizzes[this.qNum].choices[1].isCorrect == 1) {
        this.nextQuiz = false
      }
    },
    choose3: function () {
      this.answer = 3
      if (this.quizzes[this.qNum].choices[2].isCorrect == 1) {
        this.nextQuiz = false
      }
    },

    nextQ: function () {
      this.qNum += 1
      this.answer = 0
      this.nextQuiz = false
    },
  },
}
</script>

<style>
.app {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.quiz-image {
  height: 300px;
  width: 300px;
  object-fit: contain;
}

.container {
  display: flex;
  height: 2em;
  width: 300px;
  padding: 1em;
  justify-content: space-around;
}
</style>
