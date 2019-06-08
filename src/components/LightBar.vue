<template>
  <popup
    :isPopupShow="isLightShow"
    @hide-popup="hideLight"
  >
    <div class="light-wrapper">
      <div class="light-mode-wrapper">
        <div class="btn-wrapper">
          <a class="btn">护眼模式</a>
        </div>
        <div class="btn-wrapper">
          <a class="btn">夜间模式</a>
        </div>
      </div>
      <div class="light-value-wrapper">
        <div class="label-wrapper">
          <span class="label">亮度</span>
        </div>
        <div class="range-wrapper">
          <Range />
        </div>
        <div class="btn-wrapper">
          <a class="btn">系统</a>
        </div>
      </div>
    </div>
  </popup>
</template>

<script>
import Popup from './Popup'
import Range from './Range'
export default {
  props: {
    isLightShow: {
      type: Boolean,
      default: false
    }
  },
  components: {
    Popup,
    Range
  },
  methods: {
    hideLight () {
      this.$emit('hide-light')
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~styles/global';
.light-wrapper {
  padding: px2rem(10) px2rem(8);
  background-color: $barBgColor;
  font-size: px2rem(16);
  .light-mode-wrapper {
    @include menuBarItem;
    display: flex;
    justify-content: space-around;
  }
  .light-value-wrapper {
    @include menuBarItem;
    display: flex;
    align-items: center;
    .range-wrapper {
      @include center;
      flex: 1;
    }
    .label-wrapper {
      flex: 0 0 px2rem(50);
      font-size: px2rem(14);
      color: #ccc;
    }
    .btn-wrapper {
      .btn {
        padding-left: px2rem(20);
        padding-right: px2rem(20);
      }
      margin-left: px2rem(5);
    }
  }
}
</style>
