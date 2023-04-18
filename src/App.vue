<template>
  <div class="todoListBox">
    <div class="header-box">

      <div class="header-left">
        <div>+</div>
        <h2>Todo List</h2>
      </div>
      <div class="header-right">
        <button class="headerAllSelect" @click="handleAdd">添加</button>
        <button class="headerAdd" @click="handleSelectAll">全选</button>
      </div>
    </div>
    <div class="content">
      <div class="content-item" v-for="(item, index) in todoList" :key="item.id1">
        <!-- 选中 -->
        <div class="content-left" @click="handleSelect(index, item.id1)">
          <span :style="item.isCheck ? 'opacity:1' : 'opacity:0'"></span>
        </div>
        <!-- 输入框 -->
        <input type="text" class="content-input" v-model="item.text" :disabled="item.isCheck"
          :class="item.isCheck ? 'line-through' : ''">
        <!-- info -->
        <div class="content-right">
          <p>{{ item.time }}</p>
          <button @click="del(index, item.id1)">删除</button>
        </div>
      </div>
    </div>
  </div>
</template>
    
<script>
import dayjs from "dayjs"
export default {
  name: 'App',
  data() {
    return {
      todoList: [
        {
          id1: "1",
          isCheck: false, //是否选中
          text: "test",//文本内容
          time: "23-4-17-13:42" //时间
        }
      ]
    }
  },
  methods: {
    //添加功能
    handleAdd() {
      this.todoList.push({
        id1: this.randomID(),
        isCheck: false, //是否选中
        text: "",//文本内容
        time: dayjs(new Date).format("YY-MM-DD HH:mm") //时间
      })
    },
    //生成随机ID
    randomID() {
      return Number(Math.random().toString().substr(2, 0) + Date.now()).toString(10)
    },
    //删除功能
    del(index, id) {
      if (this.todoList[index].id1 === id) {
        this.todoList.splice(index, 1)
      }
    },
    //选中功能
    handleSelect(index, id) {
      // console.log(index);
      // console.log(id);
      if (this.todoList[index].id1 === id) {
        this.todoList[index].isCheck = !this.todoList[index].isCheck
      }
    },
    //全选功能
    handleSelectAll() {
      this.todoList.forEach(item => {
        item.isCheck = !item.isCheck
      })
    }
  }
}
</script>

<style lang="less">
.todoListBox {
  width: 800px;
  height: 600px;
  background-color: #3C3E4F;
  position: absolute;
  border-radius: 10px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 20px;
  box-sizing: border-box;
  color: aliceblue;

  .header-box {
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid #CCC;

    button {
      padding: 5px 10px;
      border: none;
      border-radius: 4px;
      color: #fff;
      margin-left: 10px;
    }

    .header-left {
      display: flex;
      align-items: center;

      div {
        width: 50px;
        height: 50px;
        border-radius: 50%;
        background-color: #9999E6;
        font-size: 30px;
        margin-right: 15px;
      }
    }

    .header-right {
      .headerAllSelect {
        background-color: #C43F38;
      }

      .headerAdd {
        background-color: #70B870;
      }
    }
  }

  .content {
    margin-top: 20px;
    height: 450px;
    overflow-y: scroll;

    .content-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: #6B6F70;
      margin-top: 10px;
      border-radius: 8px;
      padding: 10px 20px;
      box-sizing: border-box;

      .content-left {
        width: 30px;
        height: 30px;
        border: 1px solid #ccc;
        border-radius: 50%;
        position: relative;

        span {
          display: inline-block;
          width: 20px;
          height: 20px;
          background-color: #9a99e1;
          border-radius: 50%;
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
        }
      }



      .content-input {
        flex: 1;
        margin: 0 10px;
        outline: none;
        background-color: transparent;
        border: none;
        border-bottom: 1px solid #ccc;
        padding: 5px 10px;
        color: #fff;
      }

      .line-through {
        color: rgba(255, 255, 255, 0.5);
        text-decoration: line-through rgba(255, 255, 255, 0.8);
      }

      .content-right {
        display: flex;
        align-items: center;

        button {
          background-color: #C43F38;
          border-radius: 4px;
          margin-left: 10px;
        }
      }

    }
  }
}
</style>
