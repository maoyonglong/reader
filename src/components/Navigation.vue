<template>
  <transition name="fade">
    <div class="navigation-wrapper" v-show="isNavShow" @click="hideDirectory">
      <transition name="slide-right">
        <div class="navigation" v-show="isNavShow" @click.stop>
            <div class="tabs-wrapper">
              <div class="icon-wrapper">
                <i class="icon">&#xe601;</i>
              </div>
              <div class="icon-wrapper">
                <i class="icon">&#xe75f;</i>
              </div>
              <div class="icon-wrapper">
                <i class="icon">&#xe627;</i>
              </div>
            </div>
            <div class="directory-wrapper">
              <div
                class="directory-item-wrapper"
                v-for="(toc, idx) in navigation.toc"
                :key="idx"
              >
                <p class="title" @click="jumpTo(toc.href)">{{ toc.label }}</p>
              </div>
            </div>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    navigation: {
      type: Object,
      default: function () {
        return {
          toc: []
        }
      }
    },
    isNavShow: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    jumpTo (href) {
      this.$emit('jump-to', href)
    },
    hideDirectory () {
      this.$emit('hide-directory')
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~styles/global.scss';
.navigation-wrapper {
  position: absolute;
  z-index: 101;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(85, 85, 85, .8);
  &.fade-enter, &.fade-leave-to {
    background-color: rgba(85, 85, 85, 0);
  }
  &.fade-enter-active, &.fade-leave-active {
    transition: all .3s linear;
  }
  &.fade-enter-to, &.fade-leave {
    background-color: rgba(85, 85, 85, .8);
  }
  .navigation {
    position: absolute;
    z-index: 102;
    top: 0;
    left: 0;
    width: 90%;
    height: 100%;
    background-color: #ffe;
    &.slide-right-enter, &.slide-right-leave-to {
      transform: translateX(-100%);
    }
    &.slide-right-enter-active, &.slide-right-leave-active {
      transition: all .3s linear;
    }
    &.slide-right-enter-to, &.slide-right-leave {
      transform: translateX(0);
    }
    .tabs-wrapper {
      display: flex;
      justify-content: space-around;
      padding: px2rem(10) px2rem(30);
      background-color: #efefef;
      box-sizing: border-box;
      .icon-wrapper {
        @include center;
        .icon {
          color: #555;
        }
      }
    }
    .directory-wrapper {
      padding: px2rem(10) px2rem(20);
      .directory-item-wrapper {
        padding: px2rem(14) 0;
        font-size: px2rem(18);
        text-align: left;
        border-bottom: px2rem(1) solid #ccc;
      }
    }
  }
}
</style>
