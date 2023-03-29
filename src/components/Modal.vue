<template>
  <div class="modal-backdrop">

    <div class="modal" :style="mainStyles">
      <div class="modal-footer">
        <button type="button" class="btn-close" @click="closeSelf">关闭</button>
      </div>
      <div style="margin: 7px" id="storageInfo"></div>
      <button style="
  align-items: center;
  background: linear-gradient(45deg, #F44336, #FFEB3B, #4CAF50, #2196F3, #9C27B0);
  background-size: 400%;
  animation: rainbow 10s ease infinite;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 30px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
  letter-spacing: 1px;
  outline: none;
  text-transform: uppercase;"
              onclick="confirmClearLocalStorage()">
        清空localStorage
      </button>



      <div class="modal-header">
        <h3>我是一个Modal的标题</h3>
      </div>
      <div class="modal-body">
        我是一个Modal的标题
        <div id="api" style="display: flex;flex-flow: column;margin: 20px; ">
          <scroll-view scroll-with-animation scroll-y="true" style="width: 100%; ">

            <!-- 用来获取消息体高度 -->
            <view id="okk" scroll-with-animation>
              <!-- 消息 -->
              <view style="overflow:auto;" v-for="(x,i) in msgList" :key="i">
                <!-- 用户消息 头像可选加入-->
                <view v-if="x.my" style="display: flex;
                flex-direction: column;
                align-items: flex-end;">

                  <view style="margin: 7px; display: flex; align-items: center;">
                    <view style="border-radius: 35px;">
                      <text style="word-break: break-all;">{{x.msg}}&nbsp;&nbsp;</text>
                    </view>
                    <image src="您的头像地址哦" style="width: 40px; height: 40px; border-radius: 20px;"></image>
                    <!-- <image src="https://img2.woyaogexing.com/2017/07/07/67ca73a32fe97f63!400x400_big.jpg" style="width: 40px; height: 40px; border-radius: 80rpx;"></image> -->
                  </view>

                </view>
                <!-- 机器人消息 -->
                <view v-if="!x.my" style="display: flex;
                flex-direction: row;
                align-items: flex-start;">

                  <view style="margin: 5px; display: flex; align-items: center;">
                    <image src="机器人的头像地址哦"
                           style="width: 40px; height: 40px; border-radius: 20px;"></image>
                    <view style="border-radius: 35px;background-color: #f9f9f9;">
                      <text style="word-break: break-all;">&nbsp;&nbsp;{{x.msg}}</text>
                      <!-- &nbsp;加两个空格，美观一些 -->
                    </view>
                  </view>
                </view>
              </view>

              <view style="height: 130px;">

              </view>

            </view>
          </scroll-view>


          <!-- 底部导航栏 -->
          <view ref="toggleView" style="margin: 5px; position: relative; top: 200px;
    bottom:0px;width: 90%;display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;">
            <view style="font-size: 55px;display: flex;
        flex-direction: row;
        justify-content: space-around;
        align-items: center;width: 75%;
    margin: 20px;">

              <input v-model="msg" type="text" style="width: 75%;
            height: 45px;
            border-radius: 50px;
            padding-left: 20px;
            margin-left: 10px;background-color: #f0f0f0;" @confirm="sendMsg" confirm-type="search"
                     placeholder-class="my-neirong-sm" placeholder="用一句简短的话描述您的问题"/>
              <button @click="sendMsg" :disabled="msgLoad" style="height: 45px;
            width: 20%;;
    color: #030303;    border-radius: 2500px;">{{sentext}}
              </button>
            </view>
          </view>
          <!-- 点击按钮显示/隐藏导航栏 -->
          <button v-on:click="toggleNav"
                  style="position: fixed; bottom: 20px; right: 20px; width: 50px; height: 50px; background-color: #999; border: none; border-radius: 50%; color: #fff; font-size: 24px; text-align: center; line-height: 50px;">
            {{ navVisible ? '显' : '隐'}}
          </button>

        </div>
      </div>

    </div>

  </div>

</template>


<script scoped>
export default {
  name: `Modal`,
  props: {

  },
  data() {
    return {
    }
  },
  methods: {
    closeSelf() {
      this.$emit("closeme");
    }
  }
}

</script>
<style>

.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(0,0,0,.3);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal {
  background-color: #fff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x:auto;
  display: flex;
  flex-direction: column;
  border-radius: 16px;
  width: 700px;
}
.modal-header {
  border-bottom: 1px solid #eee;
  color: #313131;
  justify-content: space-between;
  padding: 15px;
  display: flex;
}
.modal-footer {
  border-top: 1px solid #eee;
  justify-content: flex-end;
  padding: 15px;
  display: flex;
}
.modal-body {
  position: relative;
  padding: 20px 10px;
}
.btn-close, .btn-confirm {
  border-radius: 8px;
  margin-left:16px;
  width:56px;
  height: 36px;
  border:none;
  cursor: pointer;
}
.btn-close {
  color: #313131;
  background-color:transparent;
}
.btn-confirm {
  color: #fff;
  background-color: #2d8cf0;
}

</style>
