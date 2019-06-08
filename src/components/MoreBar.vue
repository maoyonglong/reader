<template>
  <popup
    :isPopupShow="isMoreShow"
    @hide-popup="hideMore"
  >
    <div class="more-wrapper">
      <div class="more-item-wrapper" @click="toggleViewDirection">
        <div class="icon-wrapper">
          <i class="icon">&#xe631;</i>
        </div>
        <div class="text-wrapper">
          <span class="text">{{ directionLabel }}</span>
        </div>
      </div>
      <div class="more-item-wrapper">
        <div class="icon-wrapper">
          <i class="icon">&#xe75f;</i>
        </div>
        <div class="text-wrapper">
          <span class="text">书签</span>
        </div>
      </div>
      <div class="more-item-wrapper">
        <div class="icon-wrapper">
          <i class="icon">&#xe607;</i>
        </div>
        <div class="text-wrapper">
          <span class="text">分享</span>
        </div>
      </div>
      <div class="more-item-wrapper">
        <div class="icon-wrapper">
          <i class="icon">&#xe72a;</i>
        </div>
        <div class="text-wrapper">
          <span class="text">设置</span>
        </div>
      </div>
    </div>
  </popup>
</template>

<script>
import Popup from './Popup'
export default {
  props: {
    isMoreShow: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      directionLabel: '横屏'
    }
  },
  components: {
    Popup
  },
  methods: {
    hideMore () {
      this.$emit('hide-more')
    },
    toggleViewDirection () {
      const body = document.body
      if (this.directionLabel === '横屏') {
        body.style.transform = 'rotate(90deg)'
        body.style.width = window.innerHeight + 'px'
        this.directionLabel = '竖屏'
      } else {
        body.style.transform = 'rotate(0deg)'
        body.style.width = window.innerWidth + 'px'
        this.directionLabel = '横屏'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~styles/global';
.more-wrapper {
  overflow: hidden;
  background-color: $barBgColor;
  .more-item-wrapper {
    @include menuBarItem;
    display: flex;
    .icon-wrapper {
      @include center;
      flex: 0 0 px2rem(60);
      .icon {
        font-size: px2rem(24);
      }
    }
    .text-wrapper {
      display: flex;
      align-items: center;
      font-size: px2rem(14);
      color: #ccc;
    }
  }
}
</style>
