<template>
  <svg class="ball" :style="styleObject">
    <circle cx="2.5vw" cy="2.5vw" r="2.5vw" fill="#fff" />
  </svg>
</template>

<script>
export default {
  computed: {
    styleObject: function() {
      return {
        left: this.x + 'vw',
        top: this.y + 'vh',
      }
    },
  },
  props: {
    x: Number,
    y: Number,
  },
}
</script>
