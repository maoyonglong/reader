<template>
  <div class="popup-wrapper" >
    <transition name="slide-up">
      <div class="popup" v-show="isPopupShow">
        <slot></slot>
      </div>
    </transition>
    <div class="mask" v-show="isPopupShow" @click="hidePopup"></div>
  </div>
</template>

<script>
export default {
  props: {
    isPopupShow: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hidePopup () {
      this.$emit('hide-popup')
    }
  }
}
</script>

<style lang="scss" scoped>
.popup-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  .popup {
    position: absolute;
    left: 0;
    bottom: 0;
    z-index: 100;
    width: 100%;
    &.slide-up-enter, &.slide-up-leave-to {
      transform: translateY(100%);
    }
    &.slide-up-enter-active, &.slide-up-leave-active {
      transition: all .3s linear;
    }
    &.slide-up-enter-to, &.slide-up-leave {
      transform: translateY(0);
    }
  }
  .mask {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 99;
    width: 100%;
    height: 100%;
  }
}
</style>
