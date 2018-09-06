<template>
  <div class="card">
    <span :class="'left-top'">{{poker.text}}</span>
    <span :class="'right-bottom'">{{poker.text}}</span>
    <div>
      <div class="huase" v-if="poker.text!=='大王' && poker.text!=='小王'">
        <i :class="diamondClass" @click="handleHuase({huase: 'diamond', index: index})">{{poker.diamond > 1 ? poker.diamond : ''}}</i>
        <i :class="clubClass" @click="handleHuase({huase: 'club', index: index})">{{poker.club > 1 ? poker.club : ''}}</i>
        <i :class="heartClass" @click="handleHuase({huase: 'heart', index: index})">{{poker.heart > 1 ? poker.heart : ''}}</i>
        <i :class="spadeClass" @click="handleHuase({huase: 'spade', index: index})">{{poker.spade > 1 ? poker.spade : ''}}</i>
      </div>
      <div v-else class="count" @click="handleWang({index: index})">
        {{poker.count}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    poker: {
      type: Object,
      default () {
        return {
          count: 0
        }
      }
    },
    index: {
      type: Number,
      default () {
        return 0
      }
    }
  },
  computed: {
    diamondClass () {
      return this.huaseClass('diamond')
    },
    clubClass () {
      return this.huaseClass('club')
    },
    heartClass () {
      return this.huaseClass('heart')
    },
    spadeClass () {
      return this.huaseClass('spade')
    }
  },
  methods: {
    handleHuase (obj) {
      this.$emit('handleHuase', obj)
    },
    handleWang (obj) {
      this.$emit('handleWang', obj)
    },
    huaseClass (huase) {
      let clazz = `icon iconfont icon-${huase}`
      if (this.poker[huase] === 0) {
        clazz = `icon iconfont icon-${huase} gray-color`
      }
      return clazz
    }
  }
}
</script>

<style scoped>

@font-face {font-family: "iconfont";
  src: url('./fontcss/iconfont.eot?t=1535945367660'); /* IE9*/
  src: url('./fontcss/iconfont.eot?t=1535945367660#iefix') format('embedded-opentype'), /* IE6-IE8 */
  url('data:application/x-font-woff;charset=utf-8;base64,d09GRgABAAAAAAV4AAsAAAAAB/AAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAABHU1VCAAABCAAAADMAAABCsP6z7U9TLzIAAAE8AAAARAAAAFY8kEgcY21hcAAAAYAAAABfAAABlM2LNPJnbHlmAAAB4AAAAZQAAAG0nNCpmWhlYWQAAAN0AAAALwAAADYShNssaGhlYQAAA6QAAAAcAAAAJAfeA4VobXR4AAADwAAAAA4AAAAQEAAAAGxvY2EAAAPQAAAACgAAAAoBRACybWF4cAAAA9wAAAAfAAAAIAEPAE5uYW1lAAAD/AAAAUUAAAJtPlT+fXBvc3QAAAVEAAAAMwAAAEZLqCFjeJxjYGRgYOBikGPQYWB0cfMJYeBgYGGAAJAMY05meiJQDMoDyrGAaQ4gZoOIAgCKIwNPAHicY2BkYWCcwMDKwMHUyXSGgYGhH0IzvmYwYuRgYGBiYGVmwAoC0lxTGByeST3TZG7438AQw9zI0AAUZgTJAQDiXQwneJztkNEJgDAMRF+aKiJOYCcoiF9O45fTZ42aNo7hwcuRC+TjgAlQ53AyyIPQdXsqI1fWkWdO32d3IVmx2hrYHu4Svy3DU/8oM7+2Ma9v095X0Lu1EnhfWA3QFw16EHIAeJxjYGRg+N/A/I65kcGRgYHRWI5RXI6RnY+RXdwOxBIX5QPx9BjVldlAXEU7RnM7IAcsqg4UNgUKmImJm5mrAXlAKcb36qrOMloqXJzW2pIGxWbWXhxs2qqGtcWuLBIcQkJWqv8+yinyCIvyiDPrqBnWWpm7cHAE2Jvl63FxKUlpcyvIxDI3sMpKqedaGgZKqSgJiEqk2avrBcmq85tm2Lk6O1Say3ipWVZYG4TJafBLSSbbqDtligmLKIqIismbdVgb2jIAAchPPcxFzDUMmkCOmbgYGMoxsrHzMbGzgaC6mjrIwSA3m5nbQQjGh3w8HCz6HslNXKzcXB51mapMrBx8gnxcLNoOxpUuXKxsLKzutSY2GqyCzNWMnGxcBcltmRySYmzWnXMi2Nm5mZk52XnSojwaLDikeNhYrFp9whO5eGDuaWB+xtzAIAwKYzEWcVE2FnUxcUUzczYVdVMzFcYvMg2MvB6q/961WNn/229n2fbvm54JozxzQ9G9hYWzw7xqqqtqvSKm+Wx7DTQOAKvNUnR4nGNgZGBgAGJHjoIP8fw2Xxm4WRhA4Pqm09MR9P8GFgbmRiCXg4EJJAoAOWMLQQB4nGNgZGBgbvjfwBDDwgACQJKRARWwAABHCgJteJxjYWBgYEHCAACwABEAAAAAAAAAagCyANoAAHicY2BkYGBgYXBiANEMDExAzAWEDAz/wXwGAA8/AV4AeJxlj01OwzAQhV/6B6QSqqhgh+QFYgEo/RGrblhUavdddN+mTpsqiSPHrdQDcB6OwAk4AtyAO/BIJ5s2lsffvHljTwDc4Acejt8t95E9XDI7cg0XuBeuU38QbpBfhJto41W4Rf1N2MczpsJtdGF5g9e4YvaEd2EPHXwI13CNT+E69S/hBvlbuIk7/Aq30PHqwj7mXle4jUcv9sdWL5xeqeVBxaHJIpM5v4KZXu+Sha3S6pxrW8QmU4OgX0lTnWlb3VPs10PnIhVZk6oJqzpJjMqt2erQBRvn8lGvF4kehCblWGP+tsYCjnEFhSUOjDFCGGSIyujoO1Vm9K+xQ8Jee1Y9zed0WxTU/3OFAQL0z1xTurLSeTpPgT1fG1J1dCtuy56UNJFezUkSskJe1rZUQuoBNmVXjhF6XNGJPyhnSP8ACVpuyAAAAHicY2BigAAuBuyAhZGJkZmRhZGVga2ktCIzL521oDQ7VZe7OCOzIDMPxK5gYAAAi58JcgA=') format('woff'),
  url('./fontcss/iconfont.ttf?t=1535945367660') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+*/
  url('./fontcss/iconfont.svg?t=1535945367660#iconfont') format('svg'); /* iOS 4.1- */
}

.iconfont {
  font-family:"iconfont" !important;
  font-size:.2rem;
  font-style:normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.icon-diamond:before { content: "\e61b"; color: #e20000;font-size:.3rem;}

.icon-club:before { content: "\e61a"; font-size:.3rem;}

.icon-heart:before { content: "\e629"; color: #e20000; font-size:.3rem;}

.icon-spade:before { content: "\e629"; font-size:.3rem;}

.gray-color:before {
  color: #cccccc;
}

.huase{
  margin: .52rem 0 0 .14rem;
  /* display: grid;
  grid-template-rows: .5rem .5rem;
  grid-template-columns: .5rem .5rem; */
  display: flex;
  flex-wrap: wrap;
}

.huase i{
  height: .5rem;
  width: .5rem;
  line-height: .5rem;
  text-align: center;
  border: 1px solid #cccccc;
}
.count{
  line-height: 1.8rem;
  text-align: center;
}
.card{
  width: 100%;
  font-size: .3rem;
}
.left-top{
  position: absolute;
  top: 0;
  left: 5px;
}
.right-bottom{
  position: absolute;
  bottom: 0;
  right: 5px;
  transform:rotate(180deg);
}
.redColor {
  color: #e20000;
}
</style>
