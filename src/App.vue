<template>
  <el-container>
    <el-header class="header">
      <div style="margin-top: 15px;">
        <div style="width: fit-content;float: left;">
          <div class="icon">
            <svg t="1702892592527" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
              p-id="4460" data-spm-anchor-id="a313x.search_index.0.i9.1e343a81LSbmza">
              <path
                d="M568.96 459.242667l144-189.205334A382.208 382.208 0 0 0 512 213.333333c-212.074667 0-384 171.925333-384 384a382.293333 382.293333 0 0 0 93.397333 251.008l-64.554666 55.808A467.584 467.584 0 0 1 42.666667 597.333333C42.666667 338.133333 252.8 128 512 128c93.098667 0 179.861333 27.093333 252.842667 73.856l75.882666-99.690667 67.541334 51.413334-273.28 359.04a149.333333 149.333333 0 1 1-66.048-53.376z m266.453333-69.056l54.357334-71.424A467.242667 467.242667 0 0 1 981.333333 597.333333c0 113.706667-40.64 221.226667-113.237333 305.728l-64.725333-55.616A382.272 382.272 0 0 0 896 597.333333c0-76.288-22.250667-147.370667-60.586667-207.146666zM512 661.333333a64 64 0 1 0 0-128 64 64 0 0 0 0 128z"
                fill="#ffffff" p-id="4461"></path>
            </svg>
          </div>
          <span class="title"> Net-Panel </span>
        </div>
        <div style="float: right;margin-top: 5px;">
          <el-button class="home" @click="aboutVisible=true" round>关于</el-button>
        </div>
        <div v-if="isAndroid" style="float: right;margin-top: 5px;margin-right: 5px;">
          <el-button class="home" @click="downLoadAPPTableVisible=true" round></el-button>
        </div>
      </div>
    </el-header>
    <el-main>
      <MainUI :isVisible="isVisible" />
      <br>
      <IPinfoUI :isVisible="isVisible" />
    </el-main>
    <div style="height: fit-content;padding-bottom: 10px;">
      <div style="width: fit-content;margin-left: auto;margin-right: auto;">
        <el-link type="info" @click='open("https://netart.cn/")' target="_blank"></el-link>&nbsp;
        <el-link type="info" @click='open("https://github.com/ljxi/NetworkPanel")' target="_blank"></el-link>&nbsp;
        <el-link type="info" @click='open("https://github.com/ljxi/GeoCN")' target="_blank"></el-link>
      </div>
      <div style="width: fit-content;margin-left: auto;margin-right: auto;">
        <span style="color:var(--el-color-info);font-size: 12px;">
            <el-link style="vertical-align: -2px;" type="info" @click='open("")' target="_blank">
            </el-link>
        </span>
      </div>
    </div>
  </el-container>
  <el-dialog align-center style="width: 90%;max-width: 700px;" v-model="downLoadAPPTableVisible" title="">
    <div>
      <el-button style="float:right;margin-top: -5px;" type="primary" @click="open('https://api.netart.cn/d?b013x15cb')">
      </el-button> 
    </div>
  </el-dialog>
  <el-dialog style="width: 90%;max-width: 400px;" v-model="aboutVisible" title="关于">
    <div>
      <h2>Net-Panel</h2>
      <span>开源地址：<el-link @click='open("https://github.com/ljxi/NetworkPanel")' type="primary">NetworkPanel</el-link>&nbsp;
        <el-link @click='open("https://github.com/ljxi/GeoCN")' type="primary">GeoCN</el-link>
      </span><br> 
    </div>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="aboutVisible = false">关闭</el-button>
      </span>
    </template>
  </el-dialog>
</template>

<script lang="ts" setup>
import MainUI from "./components/Main.vue"
import IPinfoUI from "./components/IPinfo.vue"
import { ref, reactive, watch } from 'vue'
import { ElMessage } from 'element-plus'
import { toClipboard } from '@soerenmartius/vue3-clipboard'
var isAndroid = /Android/i.test(navigator.userAgent)
const isVisible = ref(true)
const downLoadAPPTableVisible = ref(false)
if(window.location.hash=='#app')downLoadAPPTableVisible.value=true

const clearHash=()=>{
  history.replaceState(null, document.title,
  window.location.pathname + window.location.search);
}
watch(downLoadAPPTableVisible,(n)=>{
  if(!n){
    clearHash()
  }else{
    window.location.hash='#app'
  }
})

const aboutVisible = ref(false)
const open = (url:string) => {
  window.open(url)
}

let copyText = (txt:string) => {
  toClipboard(txt)
  ElMessage.info({
    dangerouslyUseHTMLString: true,
    message: '<center>已经复制到剪切板</center>',
  })
}
document.addEventListener("visibilitychange", function () {
  var string = document.visibilityState
  if (string === 'hidden') isVisible.value = false
  else isVisible.value = true
})
</script>

<style scoped>  
.question {
  margin-top: 10px;
}
.ask {
  color: #6071ee;
}
.header {
  height: fit-content;
  padding-bottom: 12px;
  background-color: #ffffff;
}

.title {
  color: #526484;
  font-size: 20px;
  font-weight: bolder;
}

.home {
  color: #526484;
  font-size: 12px;
}
.icon {
  display:inline-block;
  vertical-align: -6px;
  width: 40px;
  height: 40px;
  background-color: #5668EE;
  border-radius: 20%;
}
.icon svg {
  width: 30px;
  margin-left: 5px;
}
.card{
    max-width: 800px;
    height:fit-content;
    display: block;
    margin:0 auto;
    background-color:#ffffff;
    padding:2%;
    border-radius: 20px;
}
.banner{
  margin-top: 15px;
}
.banner > img {
  height: 70px;
  width: calc(100% - 20px);
  margin: 10px;
  border-radius: 20px;
}
.banner > span{
  position: relative;
  display: block;
  left: 15px;
  top: 10px;
  color: transparent;
  font-weight: bolder;
  background-clip: text;
  background-image: linear-gradient(to right,#37CAC6, #3D95F4 80px);

}
@media (prefers-color-scheme: dark) {
  .card {
        background-color:rgb(18,18,18);
    }
  .header {
    background-color: rgb(18, 18, 18);
  }

  .title {
    color: rgb(152, 167, 202);
  }

  .home {
    color: rgb(152, 167, 202);
  }
}</style>
