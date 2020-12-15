<script>
export default {
  name: 'ScrollDetector',
  beforeDestroy () {
    window.removeEventListener('scroll', this.handleScroll);
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
    this.handleScroll();
  },
  data() {
    return {
      isInto: false,
    };
  },
  computed: {
  },
  methods: {
    handleScroll () {
      const rect = this.$refs.scrollDetector.getBoundingClientRect();
      const H = window.innerHeight;
      const W = window.innerWidth;
      const t = rect.top;
      const b = rect.bottom;
      const l = rect.left;
      const r = rect.right;

      const intoY = 0 <= b && H >= t || H >= t && 0 <= b;
      const intoX = 0 <= r && W >= l || W >= l && 0 <= r;

      if (!this.isInto && intoY && intoX) {
        this.isInto = true;
        this.$emit('into-client-rect');
      } else if (this.isInto && !(intoY && intoX)) {
        this.isInto = false;
        this.$emit('out-client-rect');
      }
    },
  },
};
</script>

<template>
  <div ref="scrollDetector">
    <slot></slot>
  </div>
</template>
