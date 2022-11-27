<template>
  <h1>Vue パレット</h1>
  <div>上のパレットをクリックして色を保存します.</div>
  <div>
    下のパレットを1回クリックすると, 大きなパレットにその色が表示されます.
  </div>
  <div>下のパレットを2回クリックすると, 保存した色を削除できます.</div>
  <div class="app">
    <div
      class="palette"
      v-on:mousemove="colorpick"
      v-on:click="colorselect"
      v-bind:style="paletteStyle"
    ></div>
    <p>rgba( {{ red }}, {{ green }}, 200, 0.5 )</p>
    <p>色を混ぜる</p>
    <table>
      <td>
        <button v-on:click="firstColor">1色目</button>
        <div
          v-if="DfirstColor"
          class="mini-palette"
          v-bind:style="firstColorStyle"
        ></div>
        <p v-if="DfirstColor">rgba( {{ red1 }}, {{ green1 }})</p>
      </td>
      <div>+</div>
      <td>
        <button v-on:click="secondColor">2色目</button>
        <div
          v-if="DsecondColor"
          class="mini-palette"
          v-bind:style="secondColorStyle"
        ></div>
        <p v-if="DsecondColor">rgba( {{ red2 }}, {{ green2 }})</p>
      </td>
    </table>

    <button v-on:click="fusion" v-if="Dfusion">結合！</button>
    <p v-if="Dresult">↓</p>
    <div
      v-if="Dresult"
      class="mini-palette"
      v-bind:style="mixedColorStyle"
    ></div>
    <p v-if="Dresult">rgba( {{ averagedRed }}, {{ averagedGreen }})</p>
    <div v-if="Dresult">
      <button v-on:click="keep">気に入った！</button>
      <button v-on:click="resetMixColor">もう一回！！</button>
    </div>
    <!-- 
    <button v-on:click="firstColor">1色目</button>
    <div
      v-if="DfirstColor"
      class="mini-palette"
      v-bind:style="firstColorStyle"
    ></div>
    <p v-if="DfirstColor">rgba( {{ red1 }}, {{ green1 }})</p>
    <p>+</p>
    <button v-on:click="secondColor">2色目</button>
    <div
      v-if="DsecondColor"
      class="mini-palette"
      v-bind:style="secondColorStyle"
    ></div>
    <p v-if="DsecondColor">rgba( {{ red2 }}, {{ green2 }})</p>
    <button v-on:click="fusion" v-if="Dfusion">結合！</button>
    <p v-if="Dresult">↓</p>
    <div
      v-if="Dresult"
      class="mini-palette"
      v-bind:style="mixedColorStyle"
    ></div>
    <p>rgba( {{ averagedRed }}, {{ averagedGreen }})</p>
    <div v-if="Dresult">
      <button v-on:click="keep">気に入った！</button>
      <button v-on:click="resetMixColor">もう一回！！</button>
    </div> -->

    <div class="colors-container">
      <div
        class="mini-palette"
        v-for="color in colors"
        v-bind:key="color"
        v-bind:style="{
          backgroundColor: `rgba(${color.red}, ${color.green}, 200, 0.5)`,
        }"
        v-on:click="showColor(color)"
        v-on:dblclick="deleteColor(color)"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      red: 0,
      green: 0,
      colors: [],
      num: 0,
      DfirstColor: false,
      DsecondColor: false,
      Dfusion: false,
      Dresult: false,
      red1: 0,
      green1: 0,
      red2: 0,
      green2: 0,
      averagedRed: 0,
      averagedGreen: 0,
    }
  },
  methods: {
    colorpick: function (e) {
      this.red = e.offsetX
      this.green = e.offsetY
    },
    colorselect() {
      const SelectedColor = { red: this.red, green: this.green, num: this.num }
      this.colors.push(SelectedColor)
      this.num += 1
    },
    showColor(color) {
      this.red = color.red
      this.green = color.green
      // console.log(color)
    },
    deleteColor(color) {
      this.colors.splice(color.num, 1)
      this.num -= 1
      for (let i = color.num; i < this.num + 1; ++i) {
        this.colors[i].num -= 1
      }
    },
    firstColor() {
      this.DfirstColor = true
      this.red1 = this.red
      this.green1 = this.green
      if (this.DfirstColor === true && this.DsecondColor === true) {
        this.Dfusion = true
      }
    },
    secondColor() {
      this.DsecondColor = true
      this.red2 = this.red
      this.green2 = this.green
      if (this.DfirstColor === true && this.DsecondColor === true) {
        this.Dfusion = true
      }
    },
    fusion() {
      this.averagedRed = (this.red1 + this.red2) / 2
      this.averagedGreen = (this.green1 + this.green2) / 2
      this.Dresult = true
    },
    keep() {
      const MixedColor = {
        red: this.averagedRed,
        green: this.averagedGreen,
        num: this.num,
      }
      this.colors.push(MixedColor)
      this.num += 1
    },
    resetMixColor() {
      this.DfirstColor = false
      this.DsecondColor = false
      this.Dfusion = false
      this.Dresult = false
      this.red1 = 0
      this.green1 = 0
      this.red2 = 0
      this.green2 = 0
      this.averagedRed = 0
      this.averagedGreen = 0
    },
  },
  computed: {
    paletteStyle() {
      return {
        backgroundColor: `rgba(${this.red}, ${this.green}, 200, 0.5)`,
      }
    },
    firstColorStyle() {
      return {
        backgroundColor: `rgba(${this.red1}, ${this.green1}, 200, 0.5)`,
      }
    },
    secondColorStyle() {
      return {
        backgroundColor: `rgba(${this.red2}, ${this.green2}, 200, 0.5)`,
      }
    },
    mixedColorStyle() {
      return {
        backgroundColor: `rgba(${this.averagedRed}, ${this.averagedGreen}, 200, 0.5)`,
      }
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
}
.palette {
  width: 255px;
  height: 255px;
}
.mini-palette {
  min-width: 60px;
  height: 60px;
}
.colors-container {
  display: flex;
  flex-wrap: wrap;
  width: 300px;
  padding-top: 8px;
}
</style>
