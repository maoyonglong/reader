<template>
 <div class="range" @click="changePage" @touchmove.stop.prevent="movePage" disabled="disable" ref="range">
  <div class="line-wrapper active"  ref="activeLine">
    <div class="line active"></div>
  </div>
  <div class="point-wrapper">
    <div class="point" ref="point" @touchstart.stop.prevent="enableMove" @touchend.stop.prevent="unableMove"></div>
  </div>
  <div class="line-wrapper">
    <div class="line"></div>
  </div>
 </div>
</template>

<script>
export default {
  props: {
    disable: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      moveAvailable: false
    }
  },
  methods: {
    changePage (e) {
      let curr = e.clientX - this.$refs.range.offsetLeft
      curr = curr < 0 ? 0 : curr
      let offsetWidth = this.$refs.range.offsetWidth
      let percentage = curr / offsetWidth
      let activeLineBasis = curr - this.$refs.point.offsetWidth / 2
      if (percentage > 1) {
        percentage = 1
        activeLineBasis = offsetWidth - this.$refs.point.offsetWidth / 2
      }
      let activeLine = this.$refs.activeLine
      activeLine.style.flexBasis = activeLineBasis + 'px'
      this.$emit('change-page', percentage)
    },
    movePage (e) {
      e.clientX = e.clientX || e.changedTouches[0].clientX
      if (this.moveAvailable) {
        this.changePage(e)
      }
    },
    enableMove () {
      this.moveAvailable = true
    },
    unableMove () {
      this.moveAvailable = false
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~styles/global';
.range {
  display: flex;
  width: 100%;
  .line-wrapper {
    @include center;
    flex: 1;
    .line {
      width: 100%;
      height: 1px;
      background-color: #fff;
      &.active {
        background-color: coral;
      }
    }
    &.active {
      flex: 0;
    }
  }
  .point-wrapper {
    @include center;
    .point {
      width: px2rem(12);
      height: px2rem(12);
      border-radius: 50%;
      border: px2rem(1) solid #ccc;
      background-color: #222;
    }
  }
}
</style>
