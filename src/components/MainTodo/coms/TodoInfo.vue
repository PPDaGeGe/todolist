<template>
  <div class="todo-info">
    <span class="total">{{total}}项待办</span>
    <div class="tabs">
      <a
        :class="['btn', 'primary', 'border', state == item ? 'actived' : '']"
        v-for="(item, index) in states"
        :key="index"
        @click.stop="toggle(item)"
      >{{item}}</a>
    </div>
    <button class="btn info" @click.stop='clear'>天照</button>
  </div>
</template>

<script>
  export default {
    name: 'TodoInfo',
    props:{
      total:Number
    },
    data() {
      return {
       states: ['全部', '辛德勒的名单', '死亡笔记'],
        state: '全部',
      }
    },
    methods:{
      toggle(state) {
        this.state = state
        this.$emit('toggle', state)
      },
      clear(){
        this.$emit('clear')
      }
    }
  }
</script>

<style lang="stylus" scoped>
  @import '~styles/theme.styl'
  @import '~styles/mixins.styl'

  .todo-info
    display: flex
    justify-content: space-between
    padding: 5px 10px
    font-weight: 400
    line-height: 30px
    border-top: 1px solid rgba(0, 0, 0, 0.1)
    .total
      color: $red
    .tabs
      display: flex
      justify-content: space-between
      width: 250px
    .btn.primary.border
      primaryBorderBtn()
      &.actived
        primaryBtn()
    .btn.info
      infoBtn()
</style>