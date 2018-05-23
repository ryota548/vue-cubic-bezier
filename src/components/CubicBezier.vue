<template lang='pug'>
.cubic-bezier
    svg(width="200px" height="200px" viewBox="0 0 200 200" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink")
      g.controll-area(stroke="none" stroke-width="1" fill="none" fill-rule="evenodd")
        g
          rect#Rectangle-33(fill-opacity="0" fill="#FFFFFF" x="0" y="0" width="200" height="200")
          path(
            d="M20,180 L180,20"
            id="Line-3"
            stroke-opacity="0.104761096"
            stroke="#000000" stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round")
          path(
            :d="d2"
            id="Line"
            stroke="#000000"
            stroke-width="4"
            stroke-linecap="round"
            stroke-linejoin="round")
          path(
            :d="d3"
            id="Line-2"
            stroke="#A623B8"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round")
          circle.knob(fill="#A623B8" :cx="position.x" :cy="position.y" r="8")
          circle.knob(fill="#A623B8" cx="180" cy="20" r="8")
</template>

<script>
import $ from 'jquery';
import 'jquery-ui';

export default {
  name: 'CubicBezier',
  props: ['cubicBezier'],
  computed: {
    d2() {
      return `M20,180 C${this.position.x},${this.position.y} 180,20 180,20`;
    },
    d3() {
      return `M20,180 L${this.position.x},${this.position.y}`;
    },
    position: {
      get() {
        const array = this.cubicBezier.split(',');
        return {
          x: parseInt(array[0], 0),
          y: parseInt(array[1], 0),
        };
      },
      set(val) {
        this.$emit('update', `${val.x},${val.y}`);
      },
    },
  },
  mounted() {
    $('.knob').draggable({
      start: () => {
      },
      drag: (e, ui) => {
        this.position = {
          x: ui.position.left,
          y: ui.position.top,
        };
      },
      stop: () => {
      },
    });
  },
};
</script>

<style lang='stylus' scoped>
.cubic-bezier
  width 300px
  height 300px
  background #fff
  margin-top 10px
  display flex
  align-items center
  allign-content center
  justify-content center
  .controll-area
    width 200px
    height 200px
    .knob
      position: absolute;
      &:hover
        box-shadow 0 0 0 4px rgba(166, 35, 184, 0.2)
</style>
