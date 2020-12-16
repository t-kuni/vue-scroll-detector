<script>
export default {
  name: 'ScrollDetector',
  beforeDestroy () {
    window.removeEventListener('scroll', this.handleScroll);
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);

    if (this.checkWhenMounted) {
      if (this.delayCheckWhenMounted) {
        setTimeout(() => this.handleScroll(), this.delayCheckWhenMounted);
      } else {
        this.handleScroll();
      }
    }
  },
  props: {
    checkWhenMounted: {
      type: Boolean,
      default: true,
    },
    delayCheckWhenMounted: {
      type: Number,
      default: null,
    },
    nearRange: {
      type: Number,
      default: 1,
    }
  },
  data() {
    return {
      isInto: false,
      isEnter: false,
      isNear: false,
    };
  },
  computed: {
  },
  methods: {
    handleScroll () {
      const rect = this.$refs.scrollDetector.getBoundingClientRect();

      const into = this.checkInto(rect);
      const enter = this.checkEnter(rect);
      const near = this.checkNear(rect);

      if (!this.isInto && into) {
        this.isInto = true;
        this.$emit('into-client-rect');
      } else if (this.isInto && !into) {
        this.isInto = false;
        this.$emit('out-client-rect');
      }
      if (!this.isEnter && enter) {
        this.isEnter = true;
        this.$emit('enter-client-rect');
      } else if (this.isEnter && !enter) {
        this.isEnter = false;
        this.$emit('leave-client-rect');
      }
      if (!this.isNear && near) {
        this.isNear = true;
        this.$emit('near-client-rect');
      } else if (this.isNear && !near) {
        this.isNear = false;
        this.$emit('far-client-rect');
      }
    },
    checkInto(rect) {
      const H = window.innerHeight;
      const W = window.innerWidth;
      const t = rect.top;
      const b = rect.bottom;
      const l = rect.left;
      const r = rect.right;

      const checkY = 0 <= t && H >= b || H >= b && 0 <= t;
      const checkX = 0 <= l && W >= r || W >= r && 0 <= l;

      return checkY && checkX;
    },
    checkEnter(rect) {
      const H = window.innerHeight;
      const W = window.innerWidth;
      const t = rect.top;
      const b = rect.bottom;
      const l = rect.left;
      const r = rect.right;

      const checkY = 0 <= b && H >= t || H >= t && 0 <= b;
      const checkX = 0 <= r && W >= l || W >= l && 0 <= r;

      return checkY && checkX;
    },
    checkNear(rect) {
      const EX_Y = Math.floor(window.innerHeight * this.nearRange);
      const EX_X = Math.floor(window.innerWidth * this.nearRange);
      const H = window.innerHeight;
      const W = window.innerWidth;
      const t = rect.top;
      const b = rect.bottom;
      const l = rect.left;
      const r = rect.right;

      const checkY = (0 - EX_Y) <= b && (H + EX_Y) >= t || (H + EX_Y) >= t && (0 - EX_Y) <= b;
      const checkX = (0 - EX_X) <= r && (W + EX_X) >= l || (W + EX_X) >= l && (0 - EX_X) <= r;

      return checkY && checkX;
    },
  },
};
</script>

<template>
  <div ref="scrollDetector">
    <slot></slot>
  </div>
</template>
