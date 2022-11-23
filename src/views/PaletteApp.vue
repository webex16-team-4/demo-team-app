<template>
  <h1>Vue パレット</h1>
  <div class="app">
    <div
      class="palette"
      v-on:mousemove="colorpick"
      v-on:click="colorselect"
      v-bind:style="paletteStyle"
    ></div>
    <p>rgba( {{ red }}, {{ green }}, 200, 0.5 )</p>
    <div class="colors-container">
      <div
        class="mini-palette"
        v-for="color in colors"
        v-bind:key="color"
        v-bind:style="{
          backgroundColor: `rgba(${color.red}, ${color.green}, 200, 0.5)`,
        }"
        v-on:click="showColor(color)"
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
    }
  },
  methods: {
    colorpick: function (e) {
      this.red = e.offsetX
      this.green = e.offsetY
    },
    colorselect: function () {
      const SelectedColor = { red: this.red, green: this.green }
      this.colors.push(SelectedColor)
    },
    showColor(color) {
      this.red = color.red
      this.green = color.green
      // console.log(color)
    },
  },
  computed: {
    paletteStyle() {
      return {
        backgroundColor: `rgba(${this.red}, ${this.green}, 200, 0.5)`,
      }
    },
  },
}
</script>

<style>
#app {
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
