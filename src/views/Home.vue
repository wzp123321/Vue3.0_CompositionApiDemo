<template>
  <div class="home">
    <div>{{message}}</div>
    <div class="home-header">
      <input type="text" placeholder="添加你需要做的内容" v-model="state.value"/>
      <button @click="addItem">添加</button>
    </div>
    <div class="content">
      <div class="item" v-for="(item,index) in state.todoList" :key="index">
        <span>{{item}}</span>
        <span @click="deleteItem(index)">x</span>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, computed } from '@vue/composition-api'
export default ({
  setup () {
    const state = reactive({
      todoList: [],
      value: ''
    })

    function deleteItem (index) {
      state.todoList = state.todoList.filter((item, idx) => {
        return index !== idx
      })
    }

    function addItem () {
      if (!state.value) {
        return
      }
      state.todoList.push(state.value)
      state.value = ''
    }

    // 计算属性
    const message = computed(() => {
      switch (state.todoList.length) {
        case 0:
          return '你有点懒啊'
        case 3:
          return '加油干'
        case 5:
          return '有点猛啊'
        default:
          return '继续干'
      }
    })

    return {
      state,
      deleteItem,
      addItem,
      message
    }
  }
})
</script>
<style lang="scss" scoped>
.home{
  width: 230px;
  margin: 0 auto;
  .home-header{
    padding: 5px 0;
    input{
      height: 32px;
      border: 1px solid #EDEDED;
    }
    button{
      background: #06a5ff;
      height: 32px;
      margin-left: 10px;
      border: none;
      color: #fff;
      padding: 0 10px;
      background-origin: 5px;
    }
  }
  .content{
    .item{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      padding: 10px 0;
      border-bottom: 1px solid #EDEDED;
      span{
        cursor: pointer;
        display: inline-block;
      }
    }
  }
}
</style>
