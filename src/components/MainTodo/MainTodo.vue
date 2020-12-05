<template>
    <div class="main-to">
      <input type="text" placeholder="登记目标" class="add-todo" autofocus @keyup.enter="addTodo" v-model="content" >
      <todo-item
  v-for="(item,index) in filterData"
  :key="index"
  :todo="item"
  @del="deleteItem"
></todo-item>
<todo-info :total="total" @toggle="handleToggle" @clear='clear'></todo-info>
    </div>
</template>

<script>
import TodoItem from './coms/TodoItem.vue'
import TodoInfo from './coms/TodoInfo.vue'
let id = 0
  export default {
    
      name:'MainTodo',
      data() {
        return {
        todoData: [],
        content: '',
        total: 0,
        filter: '全部',
      }
      },
      watch:{
        todoData:{
          deep:true,//当deeptrue时,数组中的对象发生变化时也会通知数据更新
          handler(){
            this.total = this.todoData.filter(item=>item.completed ==false).length 
          }
        }
      },
      computed:{
        filterData() {
        switch (this.filter) {
          case '全部':
            return this.todoData
            break
          case '辛德勒的名单':
            return this.todoData.filter((item) => item.completed == false)
            break
          case '死亡笔记':
            return this.todoData.filter((item) => item.completed == true)
            break
        }
      },
      },
      components:{
        TodoItem,
        TodoInfo
      },
      methods:{
        addTodo(){
          if(this.content ==='') return
          this.todoData.unshift({
            id:id++,
            content:this.content,
            completed:false
          })
          this.content =''
        },
        deleteItem(id){
          this.todoData.splice(
            this.todoData.findIndex(item=>item.id==id),
            1
          )
        },
        handleToggle(state) {
        this.filter = state
      },
      clear(){
        this.todoData = this.todoData.filter(item => item.completed ==false)
      }
      }
  }
</script>

<style lang="stylus" scoped>
.main-to
  margin: 0 auto
  width: 600px
  background-color: #fff
  box-shadow: 0 0 5px #666
  .add-todo
    padding: 16px 16px 16px 36px
    width: 100%
    font-size: 24px
    font-family: inherit
    font-weight: inherit
    color: inherit
    border: none
    outline: none
    box-sizing: border-box
        
</style>