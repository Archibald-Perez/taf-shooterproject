<template>
  <div class="bullet" :style="bullet.position" />
</template>

<script>
export default {
  props: {
    bullet: Object,
  },
}
</script>
