<template>
  <div class="container">
    <div class="gird-container">
      <div class="gird-item" v-for="(poker, index) in pokers" :key="index">
        <card :poker="poker" :index="index" @handleHuase="handleHuase" @handleWang="handleWang">
        </card>
      </div>
    </div>
    <div class="console">
      <div v-if="updateHistory.length > 0" class="weui-btn weui-btn_warn" @click="rollback">撤回</div>
      <div class="weui-btn weui-btn_primary" @click="setDefaultCount">{{defaultCount===1? '单':'两'}}副牌</div>
      <div v-if="updateHistory.length > 0" class="weui-btn weui-btn_warn" @click="reset">重置</div>
    </div>
    <div class="readme">
      注:
      <div> 1.可选一副牌或两副牌</div> 
      <div> 2.点击相应牌减少对应牌的数量, 数量为0时该图标变灰</div> 
      <div> 3.可撤销，撤销操作仅保留最近100个点击操作</div> 
      <div> 4.重置操作会清空所有操作记录</div>
    </div>
  </div>
</template>
<script>
import card from '@/components/card'
export default {
  components: {
    card
  },
  data () {
    const defaultCount = 1
    return {
      defaultCount: defaultCount,
      updateHistory: [],
      pokers: []
    }
  },
  watch: {
    updateHistory (oldVal, newVal) {
      if (newVal.length > 100) {
        this.updateHistory.splice(0, 1)
      }
    }
  },
  methods: {
    pokersInit () {
      this.updateHistory = []
      let defaultCount = this.defaultCount
      this.pokers = [
        {text: '3', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: '4', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: '5', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: '6', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: '7', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: '8', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: '9', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: '10', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: 'J', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: 'Q', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: 'K', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: 'A', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: '2', count: defaultCount * 4, diamond: defaultCount, club: defaultCount, heart: defaultCount, spade: defaultCount},
        {text: '小王', count: defaultCount},
        {text: '大王', count: defaultCount}
      ]
    },
    handleHuase (obj) {
      this.updateHistory.push(JSON.parse(JSON.stringify(this.pokers)))
      if (this.pokers[obj.index][obj.huase] > 0) {
        this.pokers[obj.index][obj.huase] -= 1
        this.pokers[obj.index].count -= 1
      } else {
        this.pokers[obj.index][obj.huase] = this.defaultCount
        this.pokers[obj.index].count += 1
      }
    },
    handleWang (obj) {
      this.updateHistory.push(JSON.parse(JSON.stringify(this.pokers)))
      if (this.pokers[obj.index].count > 0) {
        this.pokers[obj.index].count -= 1
      } else {
        this.pokers[obj.index].count = this.defaultCount
      }
    },
    reset () {
      this.pokersInit()
    },
    rollback () {
      let pokers = this.updateHistory[this.updateHistory.length - 1]
      this.pokers = pokers
      this.updateHistory.pop(this.updateHistory.length - 1)
    },
    setDefaultCount () {
      if (this.defaultCount === 1) {
        this.defaultCount = 2
        this.pokersInit()
      } else {
        this.defaultCount = 1
        this.pokersInit()
      }
    }
  },
  mounted () {
    this.pokersInit()
  }
}
</script>

<style scoped>
.container{
  margin-top: 1rem;
}
.gird-container{
  /* display: grid;
  grid-template-rows: 2.112rem 2.112rem 2.112rem;
  grid-template-columns: 1.368rem 1.368rem 1.368rem 1.368rem 1.368rem; */
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;
}
.gird-item{
  width: 1.368rem;
  height: 2.112rem;
  margin: 2px;
  position: relative;
  border: 1px solid #cccccc;
  border-radius: 5px;
  background-color: #FFFFFF;
}
.console{
  margin-top: 1rem;
  font-size: .3rem;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.weui-btn {
    width: 2rem;
    border-width: 0;
    outline: 0;
    -webkit-appearance: none;
    position: relative;
    display: block;
    margin-left: .2rem;
    margin-right: .2rem;
    padding-left: 14px;
    padding-right: 14px;
    box-sizing: border-box;
    text-align: center;
    text-decoration: none;
    color: #FFFFFF;
    line-height: 2.33333333;
    border-radius: 5px;
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
    overflow: hidden;
}
.weui-btn_primary {
    background-color: #1AAD19;
}
.weui-btn_warn {
    background-color: #E64340;
}
.weui-btn:after {
  content: " ";
  width: 200%;
  height: 200%;
  position: absolute;
  top: 0;
  left: 0;
  border: 1px solid rgba(0, 0, 0, 0.2);
  -webkit-transform: scale(0.5);
  transform: scale(0.5);
  -webkit-transform-origin: 0 0;
  transform-origin: 0 0;
  box-sizing: border-box;
  border-radius: 10px;
}

.readme{
  margin-top: .5rem;
  font-size: .2rem;
  color: #333333;
}
</style>
