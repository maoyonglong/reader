<template>
  <transition name="slide-down">
    <div class="title-wrapper" v-show="isBarShow">
      <div class="left">
        <div class="icon-wrapper">
          <i class="icon">&#xe731;</i>
        </div>
      </div>
      <div class="right">
        <div class="icon-wrapper">
          <i class="icon">&#xe613;</i>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    isBarShow: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~styles/global';
.title-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 100;
  display: flex;
  width: 100%;
  height: px2rem(48);
  background-color: rgba(0, 0, 0, .8);
  .left {
    flex: 0 0 px2rem(40);
    @include center;
  }
  .right {
    flex: 1;
    display: flex;
    justify-content: flex-end;
    padding-right: px2rem(20);
    box-sizing: border-box;
  }
  .icon-wrapper {
    display: flex;
    @include center;
  }
  &.slide-down-enter, &.slide-down-leave-to {
    transform: translateY(-100%);
  }
  &.slide-down-enter-active, &.slide-down-leave-active {
    transition: all .3s linear;
  }
  &.slide-down-enter-to, &.slide-down-leave {
    transform: translateY(0);
  }
}
</style>
