<script>
import Vue from 'vue';
import ScrollDetector from '@/scroll-detector.vue';

export default Vue.extend({
  name: 'ServeDev',
  data() {
    return {
      log: "aaa",
    }
  },
  components: {
    ScrollDetector
  },
  methods: {
    onIntoClientRect() {
      this.log += "into-client-rect\n";
    },
    onOutClientRect() {
      this.log += "out-client-rect\n";
    },
    onEnterClientRect() {
      this.log += "enter-client-rect\n";
    },
    onLeaveClientRect() {
      this.log += "leave-client-rect\n";
    },
    onNearClientRect() {
      this.log += "near-client-rect\n";
    },
    onFarClientRect() {
      this.log += "far-client-rect\n";
    },
  }
});
</script>

<template>
  <div id="app" style="height: 3500px; width: 5000px;">
    <pre class="log">{{ log }}</pre>
    <div style="height: 1500px;"></div>
    <div>
      <div style="display: inline-block; height: 200px; width: 2300px"></div>
      <scroll-detector @into-client-rect="onIntoClientRect"
                       @out-client-rect="onOutClientRect"
                       @enter-client-rect="onEnterClientRect"
                       @leave-client-rect="onLeaveClientRect"
                       @near-client-rect="onNearClientRect"
                       @far-client-rect="onFarClientRect"
                       :check-when-mounted="false"
                       style="display: inline-block; height: 200px; width: 400px">
        <div style="background-color: black; height: 200px; width: 400px;"></div>
      </scroll-detector>
      <div style="display: inline-block; height: 200px; width: 2300px"></div>
    </div>
    <div style="height: 1500px;"></div>
  </div>
</template>

<style scoped>
  .log {
    position: fixed;
    top: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.1);
  }
</style>