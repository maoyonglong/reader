<template>
  <popup
    :isPopupShow="isReadModeShow"
    @hide-popup="hideReadMode"
  >
    <div class="read-mode-wrapper">
      <div class="read-mode-item-wrapper">
        <h4 class="title">请选择阅读方式</h4>
      </div>
      <div class="read-mode-options-wrapper read-mode-item-wrapper">
        <div class="read-mode-option-wrapper">
          <div class="btn-wrapper">
            <a class="btn">语音朗读</a>
          </div>
        </div>
        <div class="read-mode-option-wrapper">
          <div class="btn-wrapper">
            <a class="btn">自动翻页</a>
          </div>
        </div>
      </div>
    </div>
  </popup>
</template>

<script>
import Popup from './Popup'
export default {
  props: {
    isReadModeShow: {
      type: Boolean,
      default: false
    }
  },
  components: {
    Popup
  },
  methods: {
    hideReadMode () {
      this.$emit('hide-readmode')
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~styles/global';
.read-mode-wrapper {
  // display: flex;
  // flex-direction: column;
  overflow: hidden;
  font-size: px2rem(16);
  color: #fff;
  background-color: $barBgColor;
  .title {
    padding: px2rem(10) 0;
    font-size: px2rem(14);
  }
  .read-mode-item-wrapper {
    @include menuBarItem;
  }
  .read-mode-options-wrapper {
    display: flex;
    justify-content: space-around;
  }
}
</style>
