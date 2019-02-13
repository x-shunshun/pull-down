<template>
  <div class="hello">
    <pull-down @onPullDownRefresh="onPullDownRefresh" ref="mychild">
      <div class="header">头部</div>
      <ul slot="content">
        <li v-for="(item, index) in arr" :class="{'text-right':item.length > 2}">{{item}}</li>
      </ul>
    </pull-down>
  </div>
</template>

<script>
import PullDown from './PullDown'
export default {
  name: 'index',
  data () {
    return {
      arr: [],
      word: ['你好', 'hello word', '去哪儿', '回家', '干嘛', '不干嘛', 'ok', 'thanks']
    }
  },
  components:{
    PullDown
  },
  computed: {
    
  },
  filters: {
    
  },
  created(){        
    for (let i = 0; i < 20; i++) {
      this.arr.push(this.word[Math.ceil(Math.random()*7)])
    }
  },
  mounted: function () {
 
  },
  methods:{
    onPullDownRefresh () {
      let a = []
      console.log(Math.ceil(Math.random()*10))
      let len = Math.ceil(Math.random()*10) * 5
      for (var i = 0; i < len; i++) {
        a.push(this.word[Math.ceil(Math.random()*7)])
      }
      this.arr = a.concat(this.arr)
      this.$nextTick(() => {
        console.log(document.getElementsByTagName('li'))
        console.log(document.getElementsByTagName('li')[a.length])
        console.log(document.getElementsByTagName('li')[a.length].offsetTop)
        this.$refs.mychild.changeScroll(document.getElementsByTagName('li')[a.length].offsetTop - 32);
      }) 
    },

    handleChange() {
      this.show = !this.show
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  .hello {
    
  }
  li {
    height: 50px;
    padding: 0 20px;
  }
  .text-right {
    text-align: right
  }
</style>