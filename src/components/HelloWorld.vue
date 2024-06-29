<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      colorOptions: [] as string[],
      correctIndexColor: 0,
      isGameWon: false
    }
  },
  methods: {
    generateOneChar() {
      const characters = [
        'a',
        'b',
        'c',
        'd',
        'e',
        'f',
        '1',
        '2',
        '3',
        '4',
        '5',
        '6',
        '7',
        '8',
        '9',
        '0'
      ]
      const randomChar = characters[Math.floor(Math.random() * characters.length)]
      return randomChar
    },
    generateHexacode() {
      let hexacode = '#'
      for (let i = 0; i < 6; i++) {
        hexacode += this.generateOneChar()
      }
      return hexacode
    },
    checkColor(color: string) {
      if (color === this.colorOptions[this.correctIndexColor]) {
        this.isGameWon = true
        setTimeout(this.resetGame, 2000)
      }
    },
    resetGame() {
      this.isGameWon = false
      this.colorOptions = [
        this.generateHexacode(),
        this.generateHexacode(),
        this.generateHexacode()
      ]
      this.correctIndexColor = Math.floor(Math.random() * this.colorOptions.length)
    }
  },
  created() {
    this.resetGame()
  }
})
</script>

<template>
  <h1>Color Game Vue</h1>

  <div class="box" v-bind:style="{ 'background-color': colorOptions[correctIndexColor] }"></div>

  <button
    class="color-option"
    type="button"
    v-for="colorOption in colorOptions"
    v-bind:style="{ 'background-color': colorOption }"
    v-bind:key="colorOption"
    v-on:click="checkColor(colorOption)"
  >
    {{ colorOption }}
  </button>

  <p v-if="isGameWon">Jeu gagné !</p>
</template>

<style>
.box {
  width: 200px;
  height: 200px;
}
.color-option {
  width: 100px;
  height: 40px;
}
</style>
