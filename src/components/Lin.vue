<template>
  <div :style="styleObject" class="line">
    <svg viewBox="0 0 6 6">
      <line x1="1" y1="3" x2="5" y2="3" stroke="#fff" stroke-linecap="round" />
      <path d="M1,3 h4" stroke="#fff" stroke-width="0.025" />
    </svg>
  </div>
</template>

<script>
export default {
  computed: {
    styleObject: function() {
      return {
        left: 'calc(' + this.x + 'vw + 5000vw + 50vw - 14vw / 2)',
        top: 'calc(' + this.y + 'vw + 5000vw + 50vh - 14vw / 2)',
      }
    },
  },
  props: {
    x: Number,
    y: Number,
  },
}
</script>
