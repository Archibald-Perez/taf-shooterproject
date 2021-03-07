<template>
  <div
    class="game"
    @keydown="keypress"
    @keyup="keypress"
    tabindex="0"
    ref="game"
  >
    <Bullet
      v-for="bullet in bulletsVisible"
      :key="bullet.index"
      :bullet="bullet"
      @kill="destroyBullet(bullet)"
    />
    <Ship class="player-ship" :x="x" :y="y" />
    <Ship :x="30" :y="50" :bullets="bulletsVisible" :move="true" />
    <Ship :x="20" :y="50" :bullets="bulletsVisible" :move="true" />
    <Ship :x="40" :y="70" :bullets="bulletsVisible" :move="true" />
    <Ship :x="60" :y="20" :bullets="bulletsVisible" :move="true" />
  </div>
</template>

<script>
import Bullet from './Bullet.vue'
import Ship from './Ship.vue'
export default {
  data() {
    return {
      keys: Array(41).fill(false),
      speed: -0.3,
      speedX: 0,
      speedY: 0,
      x: 47.5,
      y: 85,
      bullets: [],
      bulletDelay: 0,
      bulletIndex: 0,
    }
  },
  components: {
    Bullet,
    Ship,
  },
  computed: {
    bulletsVisible() {
      return this.bullets.filter((bullet) => bullet.show)
    },
  },
  methods: {
    destroyBullet(bulletIndex) {
      this.bullets[bulletIndex].show = false
    },
    keypress(key) {
      this.keys[key.keyCode] = key.type == 'keydown'
    },
    updateGame() {
      // Ship position
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
      // Add bullets
      if (this.keys[32]) {
        if (this.bulletDelay > 10) {
          this.bullets.push({
            position: {
              left: this.x + 'vw',
              top: this.y + 'vh',
            },
            posX: this.x,
            posY: this.y,
            startY: this.y,
            index: this.bulletIndex,
            time: 0,
            show: true,
          })
          this.bulletIndex++
          this.bulletDelay = 0
        } else {
          this.bulletDelay++
        }
      }
      // Bullets positions
      for (let bullet of this.bulletsVisible) {
        bullet.time++
        bullet.position.top = bullet.startY - bullet.time + 'vh'
        bullet.posY = bullet.startY - bullet.time
        if (bullet.time > 100) {
          this.destroyBullet(bullet.index)
        }
      }
    },
  },
  mounted() {
    setInterval(this.updateGame, 10)
    this.$refs.game.focus()
  },
}
</script>
