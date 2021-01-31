<template>
  <div :style="styleObject" class="background">
    <Lin :x="x" :y="y" />
  </div>
</template>

<script>
import Lin from './Lin.vue'
export default {
  computed: {
    styleObject: function() {
      return {
        left: this.x + 'vw',
        top: this.y + 'vw',
      }
    },
  },
  props: {
    x: Number,
    y: Number,
  },
  components: {
    Lin,
  },
}
</script>
