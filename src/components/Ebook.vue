<template>
 <div class="ebook">
  <title-bar
    :isBarShow="isBarShow"
  />
  <div class="read-wrapper">
    <div id="epub"></div>
    <div class="mask">
      <div class="mask-left" @click="prev"></div>
      <div class="mask-middle" @click="toggleBar"></div>
      <div class="mask-right" @click="next"></div>
    </div>
  </div>
  <menu-bar
    @change-page="changePage"
    @show-directory="showDirectory"
    @show-option="showOption"
    @show-light="showLight"
    @show-readmode="showReadMode"
    @show-more="showMore"
    :isBarShow="isBarShow"
    :bookAvailable="bookAvailable"
  />
  <navigation
    @jump-to="jumpTo"
    @hide-directory="hideDirectory"
    :navigation="navigation"
    :isNavShow="isNavShow"
  />
  <option-bar
    :isOptionShow="isOptionShow"
    :fontSizes="fontSizes"
    :defaultFontSizeIdx="defaultFontSizeIdx"
    @hide-option="hideOption"
    @set-fontsize="setFontSize"
    @set-theme="setTheme"
    @set-fontfamily="setFontFamily"
  />
  <light-bar
    :isLightShow="isLightShow"
    @hide-light="hideLight"
  />
  <read-mode-bar
    :isReadModeShow="isReadModeShow"
    @hide-readmode="hideReadMode"
  />
  <more-bar
    :isMoreShow="isMoreShow"
    @hide-more="hideMore"
  />
 </div>
</template>

<script>
import Epub from 'epubjs'
import TitleBar from './TitleBar'
import MenuBar from './MenuBar'
import Navigation from './Navigation'
import OptionBar from './OptionBar'
import LightBar from './LightBar'
import ReadModeBar from './ReadModeBar'
import MoreBar from './MoreBar'
const EPUB_URL = '/static/test.epub'
export default {
  data () {
    return {
      isBarShow: false,
      isNavShow: false,
      bookAvailable: false,
      navigation: {},
      isOptionShow: false,
      isLightShow: false,
      isReadModeShow: false,
      isMoreShow: false,
      fontSizes: [12, 14, 16, 18, 20, 22, 24, 26],
      defaultFontSizeIdx: 2,
      themesList: [
        {
          name: 'pink',
          content: {
            body: {
              'background-color': 'lightpink',
              color: '#000'
            }
          }
        },
        {
          name: 'orange',
          content: {
            body: {
              'background-color': 'lightsalmon',
              color: '#000'
            }
          }
        },
        {
          name: 'green',
          content: {
            body: {
              'background-color': 'lightgreen',
              color: '#000'
            }
          }
        },
        {
          name: 'gray',
          content: {
            body: {
              'background-color': 'gray',
              color: '#fff'
            }
          }
        }
      ]
    }
  },
  components: {
    MenuBar,
    TitleBar,
    Navigation,
    OptionBar,
    LightBar,
    ReadModeBar,
    MoreBar
  },
  methods: {
    registerThemes () {
      this.themesList.forEach(theme => {
        this.themes.register(theme.name, theme.content)
      })
    },
    setTheme (idx) {
      console.log(this.themesList[idx].name)
      this.themes.select(this.themesList[idx].name)
    },
    setFontFamily (family) {
      this.themes.font(family)
    },
    setFontSize (fontSize, idx) {
      this.defaultFontSizeIdx = idx
      this.themes.fontSize(fontSize + 'px')
    },
    showEpub () {
      this.book = new Epub(EPUB_URL)
      this.rendition = this.book.renderTo('epub', {
        width: window.innerWidth,
        height: window.innerHeight
      })
      this.themes = this.rendition.themes
      this.registerThemes()
      this.setFontSize(this.fontSizes[this.defaultFontSizeIdx])
      this.rendition.display()
      this.book.ready.then(() => {
        this.navigation = this.book.navigation
        return this.book.locations.generate()
      }).then(result => {
        this.locations = this.book.locations
        this.bookAvailable = true
      })
    },
    prev () {
      this.rendition.prev()
      this.hideBar()
    },
    next () {
      this.rendition.next()
      this.hideBar()
    },
    changePage (percentage) {
      this.rendition.display(this.locations.cfiFromPercentage(percentage))
    },
    jumpTo (href) {
      this.rendition.display(href)
      this.hideDirectory()
    },
    hideBar () {
      this.isBarShow = false
    },
    toggleBar () {
      this.isBarShow = !this.isBarShow
    },
    showDirectory () {
      this.hideBar()
      this.isNavShow = true
    },
    hideDirectory () {
      this.isNavShow = false
    },
    showOption () {
      this.isOptionShow = true
      this.hideBar()
    },
    hideOption () {
      this.isOptionShow = false
    },
    showLight () {
      this.isLightShow = true
      this.hideBar()
    },
    hideLight () {
      this.isLightShow = false
    },
    showReadMode () {
      this.isReadModeShow = true
      this.hideBar()
    },
    hideReadMode () {
      this.isReadModeShow = false
    },
    showMore () {
      this.isMoreShow = true
      this.hideBar()
    },
    hideMore () {
      this.isMoreShow = false
    }
  },
  mounted () {
    this.showEpub()
  }
}
</script>

<style lang="scss" scoped>
@import '~styles/global';
.ebook {
  position: relative;
  .read-wrapper {
    .mask {
      position: absolute;
      display: flex;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 99;
      &-left {
        flex: 0 0 px2rem(40);
      }
      &-middle {
        flex: 1;
      }
      &-right {
        flex: 0 0 px2rem(40);
      }
    }
  }
}
</style>
