<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. {{ quizzes[qNum].text }}</h2>
    <img v-bind:src="imgS" class="quiz-image" alt="クイズタイトル" />
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

    <div>答え</div>
    <div v-if="answer == 0">
      <div v-if="quizzes[qNum].choices[answer].isCorrect == 1">正解！</div>
      <div v-if="quizzes[qNum].choices[answer].isCorrect == 0">不正解！</div>
      <div>{{ quizzes[qNum].choices[answer].feedback }}</div>
    </div>
    <div v-if="answer == 1">
      <div v-if="quizzes[qNum].choices[answer].isCorrect == 1">正解！</div>
      <div v-if="quizzes[qNum].choices[answer].isCorrect == 0">不正解！</div>
      <div>{{ quizzes[qNum].choices[answer].feedback }}</div>
    </div>
    <div v-if="answer == 2">
      <div v-if="quizzes[qNum].choices[answer].isCorrect == 1">正解！</div>
      <div v-if="quizzes[qNum].choices[answer].isCorrect == 0">不正解！</div>
      <div>{{ quizzes[qNum].choices[answer].feedback }}</div>
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
      qNum: 0, //問題番号。0番が最初の問題
      answer: -1, //答えの部分に表示する正誤と解説を指定するのに使う
      nextQuiz: false, //正解の選択肢が選ばれたかどうかを判定するのに使う
      //以下、クイズの内容
      quizzes: [
        //1問目
        {
          text: "G(ギガ)の1000倍はT(テラ)。ではT(テラ)の1000倍は？", //問題文
          image: "tera.png", //問題の画像(ファイル名のみ)
          //選択肢3つ
          choices: [
            {
              text: "Z(ゼタ)", //選択ボタンに表示する内容
              isCorrect: 0, //正解かどうか。正解は1、不正解は0
              feedback: "Z(ゼタ)は10の21乗です！", //選択肢が選ばれた後に表示する解説
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
          image: "train.png",
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
      imgS: require("@/assets/tera.png"), //表示する画像のパスを持っておく変数
    }
  },

  methods: {
    //左の選択肢が選ばれたときの処理
    choose1: function () {
      this.answer = 0
      if (this.quizzes[this.qNum].choices[0].isCorrect == 1) {
        this.nextQuiz = true
      } else {
        this.nextQuiz = false
      }
    },
    //真ん中の選択肢が選ばれたときの処理
    choose2: function () {
      this.answer = 1
      if (this.quizzes[this.qNum].choices[1].isCorrect == 1) {
        this.nextQuiz = true
      } else {
        this.nextQuiz = false
      }
    },
    //右の選択肢が選ばれたときの処理
    choose3: function () {
      this.answer = 2
      if (this.quizzes[this.qNum].choices[2].isCorrect == 1) {
        this.nextQuiz = true
      } else {
        this.nextQuiz = false
      }
    },

    //次の問題に行くボタンが押されたときの処理
    nextQ: function () {
      if (this.qNum !== this.quizzes.length - 1) {
        this.qNum += 1
      } else {
        this.qNum = 0
      }
      this.answer = -1
      this.nextQuiz = false
      this.imgS = require("@/assets/" + this.quizzes[this.qNum].image)
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
