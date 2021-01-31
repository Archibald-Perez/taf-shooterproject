<template>
  <div
    class="game"
    @keydown="keypress"
    @keyup="keypress"
    tabindex="0"
    ref="game"
  >
    <Ball />
    <Board :x="x" :y="y" />
  </div>
</template>

<script>
import Ball from './Ball.vue'
import Board from './Board.vue'
export default {
  data() {
    return {
      keys: Array(41).fill(false),
      speed: -0.3,
      speedX: 0,
      speedY: 0,
      x: 47.5,
      y: 85,
    }
  },
  components: {
    Ball,
    Board,
  },
  methods: {
    keypress(key) {
      this.keys[key.keyCode] = key.type == 'keydown'
    },
    updateGame() {
      this.speedX = 0
      this.speedY = 0
      if (this.keys[37]) {
        this.speedX += this.speed
      }
      if (this.keys[39]) {
        this.speedX += -this.speed
      }
      if (this.keys[38]) {
        this.speedY += this.speed
      }
      if (this.keys[40]) {
        this.speedY += -this.speed
      }
      this.x += this.speedX
      this.y += this.speedY
      this.x = Math.min(Math.max(this.x, 5), 95)
      this.y = Math.min(Math.max(this.y, 5), 95)
    },
  },
  mounted() {
    setInterval(this.updateGame, 10)
    this.$refs.game.focus()
  },
}
</script>
