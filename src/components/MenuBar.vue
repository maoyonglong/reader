<template>
  <transition name="slide-up">
    <div class="menu-wrapper" v-show="isBarShow">
      <div class="top">
        <div class="text-wrapper">
          <span class="text">上一章</span>
        </div>
        <div class="range-wrapper">
          <range @change-page="changePage" :disable="bookAvailable"/>
        </div>
        <div class="text-wrapper">
          <span class="text">下一章</span>
        </div>
      </div>
      <div class="bottom">
        <div class="item-wrapper"  @click="showDirectory">
          <div class="icon-wrapper">
            <i class="icon">&#xe601;</i>
          </div>
          <div class="text-wrapper">目录</div>
        </div>
        <div class="item-wrapper" @click="showOption">
          <div class="icon-wrapper">
            <i class="icon">&#xe636;</i>
          </div>
          <div class="text-wrapper">选项</div>
        </div>
        <div class="item-wrapper" @click="showLight">
          <div class="icon-wrapper">
            <i class="icon">&#xe634;</i>
          </div>
          <div class="text-wrapper">亮度</div>
        </div>
        <div class="item-wrapper" @click="showReadMode">
          <div class="icon-wrapper">
            <i class="icon">&#xe63f;</i>
          </div>
          <div class="text-wrapper">阅读模式</div>
        </div>
        <div class="item-wrapper" @click="showMore">
          <div class="icon-wrapper">
            <i class="icon">&#xe600;</i>
          </div>
          <div class="text-wrapper">更多</div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import Range from './Range'
export default {
  props: {
    isBarShow: {
      type: Boolean,
      default: false
    },
    bookAvailable: {
      type: Boolean,
      default: false
    }
  },
  components: {
    Range
  },
  methods: {
    changePage (percentage) {
      this.$emit('change-page', percentage)
    },
    showDirectory () {
      this.$emit('show-directory')
    },
    showOption () {
      this.$emit('show-option')
    },
    showLight () {
      this.$emit('show-light')
    },
    showReadMode () {
      this.$emit('show-readmode')
    },
    showMore () {
      this.$emit('show-more')
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~styles/global';
.menu-wrapper {
  position: absolute;
  flex-direction: column;
  display: flex;
  bottom: 0;
  left: 0;
  z-index: 100;
  width: 100%;
  background-color: rgba(0, 0, 0, .8);
  &.slide-up-enter, &.slide-up-leave-to {
    transform: translateY(100%);
  }
  &.slide-up-enter-active, &.slide-up-leave-active {
    transition: all .3s linear;
  }
  &.slide-up-enter-to, &.slide-up-leave {
    transform: translateY(0);
  }
  .top {
    display: flex;
    height: px2rem(48);
    .text-wrapper {
      @include center;
      flex: 0 0 px2rem(80);
      .text {
        font-size: px2rem(14);
        color: #ccc;
      }
    }
    .range-wrapper {
      @include center;
      flex: 1;
    }
  }
  .bottom {
    display: flex;
    .item-wrapper {
      flex: 1;
      .icon-wrapper {
        @include center;
        padding: px2rem(10);
        box-sizing: border-box;
      }
      .text-wrapper {
        @include center;
        font-size: px2rem(8);
        color: #fff;
        padding-bottom: px2rem(20);
        box-sizing: border-box;
      }
    }
  }
}
</style>
