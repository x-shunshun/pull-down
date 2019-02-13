<template>
  <div class="main">
    <div class="box" @touchstart="touchStart($event)" @touchmove="touchMove($event)" @touchend="touchEnd($event)">
      <div class="loading">{{top > 5 ? '正在加载...' : '下拉加载更多'}}</div>
      <slot name="content"></slot>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      pageY: 0,
      top: 0
    }
  },
  created(){

  },
  mounted: function () {
    this.$nextTick(() => {
      setTimeout(() => {
        console.log(document.documentElement.scrollHeight)
        console.log(document.body.scrollHeight)
        console.log(document.documentElement.scrollHeight || document.body.scrollHeight)
        window.scrollTo(0, document.documentElement.scrollHeight || document.body.scrollHeight)
      }, 200)
    })
  },
  methods:{
    touchStart (e) {
      this.pageY = e.targetTouches[0].pageY
    },

    touchMove (e) {
      console.log('this.top',this.top)
      console.log(document.documentElement.scrollTop)
      console.log(document.body.scrollTop)
      if (e.targetTouches[0].pageY > this.pageY) {
        if (document.documentElement.scrollTop === 0 || document.body.scrollTop === 0) {
          this.top += 0.5
          document.getElementsByClassName('box')[0].style.transform = 'translateY('+this.top+'px)'
        }
      }
    },

    touchEnd (e) {
      if (this.top > 5) {
        this.$emit('onPullDownRefresh')
      }
      this.returnNormal()
    },

    returnNormal () {
      this.top = 0
      document.getElementsByClassName('box')[0].style.transitionDuration = '200ms'
      document.getElementsByClassName('box')[0].style.transform = 'translateY(-32px)'
      setTimeout(() => {
        document.getElementsByClassName('box')[0].style.transitionDuration = '0s'
      }, 200)
    },

    changeScroll (top) {
      console.log(top)
      document.documentElement.scrollTop = top
      document.body.scrollTop = top
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  .loading {
    height: 32px;
    text-align: center;
    line-height: 32px;
  }
  .box {
    transform: translateY(-32px);
    transition-duration: 0s;
  }
</style>