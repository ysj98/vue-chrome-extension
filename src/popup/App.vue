<template>
  <div id="app">
    <!-- <el-header height="24">B站小工具</el-header>
      <el-main>
        <el-row :gutter="5">
          <el-input
            type="textarea"
            :rows="2"
            placeholder="请输入内容"
            v-model="message"
            class="mb-5"
          >
          </el-input>

          <div>
            <el-button @click="addComment">评论</el-button>
          </div>
      </el-main> -->
    <el-tabs style="width: 100%; height: 380px" v-model="active" @tab-click="handleClick" :stretch="true" type="border-card" :tab-position="tabPosition">
      <el-tab-pane v-for="(item, index) in nodeList" :key="index" :label="item.name" :name="item.key">
        <components :is="item.key"></components>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import power from '@/components/power.vue'
import platform from '@/components/platform.vue'
import proxy from '@/components/proxy.vue'
import author from '@/components/author.vue'

export default {
  name: 'App',
  components: { power, platform, proxy, author },
  data() {
    return {
      tabPosition: 'left',
      message: '',
      list: [],
      open: false,
      nodeList: [
        { name: '开启所有权限', key: 'power' },
        { name: '平台切换', key: 'platform' },
        { name: 'config.js文件代理', key: 'proxy' },
        { name: 'Author', key: 'author' },
      ],
      active: 'power',
    }
  },
  created() {
    chrome.storage.sync.get('list', obj => {
      this.list = obj['list']
    })
  },
  mounted() {
    chrome.runtime.onMessage.addListener(function (request, sender, sendResponse) {
      console.log('收到来自content-script的消息：')
      console.log(request, sender, sendResponse)
      sendResponse('我是后台，我已收到你的消息：' + JSON.stringify(request))
    })
  },
  methods: {
    handleClick(tab, event) {
      console.log('🚀 ~ file: App.vue ~ line 66 ~ handleClick ~ tab', tab)
      // this.active = tab
    },
    sendMessageToContentScript(message, callback) {
      chrome.tabs.query({ active: true, currentWindow: true }, function (tabs) {
        chrome.tabs.sendMessage(tabs[0].id, message, function (response) {
          if (callback) callback(response)
        })
      })
    },
    addComment() {
      this.sendMessageToContentScript({ cmd: 'addComment', message: this.message }, function () {
        console.log('来自content的回复：' + response)
      })
    },
  },
}
</script>

<style>
html {
  width: 400px;
  height: 400px;
}

.el-header,
.el-footer {
  background-color: #b3c0d1;
  color: #333;
  text-align: center;
  line-height: 24px;
  font-size: 16px;
}

.el-main {
  display: block;
  flex: 1;
  flex-basis: auto;
  overflow: auto;
  box-sizing: border-box;
  padding: 5px;
}

.el-row {
  padding: 5px 0;
}
</style>
