<template>
 <popup
    :isPopupShow="isOptionShow"
    @hide-popup="hideOption"
  >
    <div class="option-wrapper">
      <div class="option-item-wrapper">
        <span class="option-name">字号</span>
        <div class="option-content">
          <a class="btn" @click="setFontSize(-1)">小</a>
          <a class="btn" @click="setFontSize(1)">大</a>
        </div>
      </div>
      <div class="option-item-wrapper">
        <span class="option-name">字体</span>
        <div class="option-content">
          <a class="btn">繁体</a>
          <a class="btn">更改字体</a>
        </div>
      </div>
      <div class="option-item-wrapper">
        <span class="option-name">排版</span>
        <div class="option-content">
          <div class="icon-wrapper">
            <i class="icon">&#xe611;</i>
          </div>
          <div class="icon-wrapper">
            <i class="icon">&#xe615;</i>
          </div>
          <div class="icon-wrapper">
            <i class="icon">&#xe612;</i>
          </div>
          <div class="circle-btn">
            <span>无</span>
          </div>
          <a class="small-btn">自定义排版</a>
        </div>
      </div>
      <div class="option-item-wrapper">
        <span class="option-name">排版</span>
        <div class="option-content">
          <a class="bg-btn pink" @click="setTheme(0)"></a>
          <a class="bg-btn orange" @click="setTheme(1)"></a>
          <a class="bg-btn green" @click="setTheme(2)"></a>
          <a class="bg-btn gray" @click="setTheme(3)"></a>
          <a class="small-btn">更多</a>
        </div>
      </div>
    </div>
  </popup>
</template>

<script>
import Popup from './Popup'
export default {
  props: {
    isOptionShow: {
      type: Boolean,
      default: true
    },
    fontSizes: {
      type: Array,
      default () {
        return []
      }
    },
    defaultFontSizeIdx: {
      type: Number,
      default: 0
    }
  },
  components: {
    Popup
  },
  methods: {
    hideOption () {
      this.$emit('hide-option')
    },
    setFontSize (distance) {
      let nextIdx = this.curFontSizeIdx + distance
      if (nextIdx >= 0 && nextIdx < this.fontSizeLen) {
        this.curFontSizeIdx = nextIdx
        this.$emit('set-fontsize', this.fontSizes[nextIdx], nextIdx)
      }
    },
    setTheme (idx) {
      this.$emit('set-theme', idx)
    }
  },
  created () {
    this.fontSizeLen = this.fontSizes.length
    this.curFontSizeIdx = this.defaultFontSizeIdx
  }
}
</script>

<style lang="scss" scoped>
@import '~styles/global';
@mixin btn {
  margin: px2rem(10);
  padding: px2rem(8) 0;
  color: #fff;
  border: px2rem(1) solid #fff;
  border-radius: px2rem(20);
  box-sizing: border-box;
}
.circle-btn {
  @include btn;
  flex: 0 0 px2rem(30);
  height: px2rem(30);
  margin-right: px2rem(4);
  border-radius: 50%;
}
.option-wrapper {
  background-color: rgba(0, 0, 0, .8);
  padding: px2rem(10) px2rem(8);
  .option-item-wrapper {
    display: flex;
    align-items: center;
    .option-name {
      flex: 0 0 px2rem(40);
      margin-right: px2rem(20);
      font-size: px2rem(14);
      color: #fff;
    }
    .option-content {
      display: flex;
      justify-content: space-around;
      align-items: center;
      flex: 1;
      .btn {
        display: block;
        flex: 1;
        text-align: center;
        font-size: px2rem(15);
        @include btn;
      }
      .icon-wrapper {
        display: flex;
        @include center;
        @extend .circle-btn;
        .icon {
          font-size: px2rem(12);
        }
      }
      .circle-btn {
        @include center;
        font-size: px2rem(12);
      }
      .small-btn {
        @include btn;
        flex: 0 0 px2rem(100);
        font-size: px2rem(15);
      }
      .bg-btn {
        @extend .circle-btn;
        &.pink {
          background-color: lightpink;
        }
        &.orange {
          background-color: lightsalmon;
        }
        &.green {
          background-color: lightgreen;
        }
        &.gray {
          background-color: gray;
        }
      }
    }
  }
}
</style>
