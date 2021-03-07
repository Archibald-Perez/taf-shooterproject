<template>
  <div class="ship" :style="position" />
</template>

<script>
export default {
  data() {
    return {
      time: 0,
      isDead: false,
    }
  },
  computed: {
    newPosX: function() {
      return this.x + this.time / 10
    },
    position: function() {
      if (this.move) {
        return {
          left: this.newPosX + 'vw',
          top: this.y + 'vh',
          display: this.isDead ? 'none' : 'fail',
        }
      } else {
        return {
          left: this.x + 'vw',
          top: this.y + 'vh',
          display: this.isDead ? 'none' : 'fail',
        }
      }
    },
  },
  methods: {
    routine: function() {
      this.time++
      if (this.bullets) {
        for (const bullet of this.bullets) {
          if (
            this.newPosX < bullet.posX + 1 &&
            this.newPosX + 2.5 > bullet.posX &&
            this.y < bullet.posY + 1 &&
            this.y + 2.5 > bullet.posY
          ) {
            this.isDead = true
          }
        }
      }
    },
  },
  props: {
    x: Number,
    y: Number,
    bullets: Array,
    move: Boolean,
  },
  mounted() {
    this.routine
    setInterval(this.routine, 10)
  },
}
</script>
