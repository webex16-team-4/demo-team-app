<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. {{ quizzes[qNum].text }}</h2>
    <img
      class="quiz-image"
      v-bind:src="quizzes[qNum].image"
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

    <div>{{ "答え" }}</div>
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
          text: "G(ギガ)の1000倍はT(テラ)。ではT(テラ)の1000倍は？",
          image: "@/assets/tera.png",
          choices: [
            {
              text: "Z(ゼタ)",
              isCorrect: 0,
              feedback: "Z(ゼタ)は10の21乗です！",
            },
            {
              text: "E(エクサ)",
              isCorrect: 0,
              feedback: "E(エクサ)は10の18乗です！",
            },
            {
              text: "P(ペタ)",
              isCorrect: 1,
              feedback: "P(ペタ)は10の15乗です！",
            },
          ],
        },
        //2問目
        {
          text: "日本で一番最初に鉄道が開通したのはどの区間？",
          image: "@/assets/train.png",
          choices: [
            {
              text: "新橋-横浜間",
              isCorrect: 1,
              feedback: "平均時速は32km/hで、50分かかったみたい！",
            },
            {
              text: "新橋-東京",
              isCorrect: 0,
              feedback: "おしい！新橋とどこだろう？",
            },
            {
              text: "横浜-鎌倉間",
              isCorrect: 0,
              feedback: "開通させるならもっと人口密度が高いところが良いかも！",
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
      } else {
        this.nextQuiz = false
      }
    },
    choose2: function () {
      this.answer = 2
      if (this.quizzes[this.qNum].choices[1].isCorrect == 1) {
        this.nextQuiz = true
      } else {
        this.nextQuiz = false
      }
    },
    choose3: function () {
      this.answer = 3
      if (this.quizzes[this.qNum].choices[2].isCorrect == 1) {
        this.nextQuiz = true
      } else {
        this.nextQuiz = false
      }
    },

    nextQ: function () {
      if (this.qNum !== this.quizzes.length - 1) {
        this.qNum += 1
      } else {
        this.qNum = 0
      }
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
  width: 400px;
  padding: 1em;
  justify-content: space-around;
}
</style>
