<script setup>

import {onMounted, ref} from 'vue';
import {mesaages} from "@/apis/mesaage.js";

const currentPage = ref(1)
const total = ref(100)

const messages = ref([])

const getMessages = async () => {
  const res = await mesaages(currentPage.value)
  //console.log("res", res.data.messages)
  messages.value = res.data.messages
}

onMounted(()=>{
  getMessages()
})
</script>
<template>

  <el-container>
    <el-main class="personal-main-outer-box">


      <div class="content">

        <el-row>

<!--          <div class="count-operate">

            <div class="count">
              <span>12条消息，2条未读</span>
            </div>

            <div class="operate">
              <button class="operate-bt">
                <i style="margin-right: 5px" class="iconfont icon-shanchu"></i>
                全部标记为已读
              </button>
            </div>

          </div>-->

          <el-col :span="24" v-for="item in messages" :key="item">
            <div class="col">
              <p>
                <span>{{item.createdAt}}</span>
              </p>
              <div class="message-content">
                <p>{{item.title}}</p>
                <p>{{item.content}}！</p>
              </div>
            </div>
          </el-col>

        </el-row>

      </div>

    </el-main>
  </el-container>
</template>

<style lang="less" scoped>
.personal-main-outer-box {

  /deep/ .el-row {
    margin-top: 20px;
  }


  .top {
    border-bottom: 1px solid #beb9b9;
    padding-bottom: 10px;
  }

  .main {
    padding: 20px;

    width: 70%;
    margin-left: 15%;

    .select {
      display: flex;
      justify-content: center;
      width: 80%;
      margin-left: 10%;
    }

    .select {
      padding-bottom: 3%;
      padding-top: 3%;
      border-bottom: 1px solid #beb9b9;
    }

    .content {
      width: 100%;


      .count-operate {
        display: flex;
        justify-content: space-between;
        width: 100%;
        margin-bottom: 2%;
        align-items: center;

        .operate {
          .operate-bt {
            font-size: 15px;
            padding: 8px 15px;
            border-radius: 20px;
            border: 1px solid #beb9b9;
          }
        }
      }

      .col {

        .col-bottom {
          display: flex;
          justify-content: flex-end;
          margin-top: 2%;
          border-top: 1px solid #beb9b9;
          padding: 2% 2%;
        }

        padding: 0.5% 2%;
        margin-bottom: 1%;

        border: 1px solid #beb9b9;
        border-radius: 20px;

      }

    }
  }
}
</style>