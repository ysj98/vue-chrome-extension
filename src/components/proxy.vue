<template>
  <div class="proxy">
    <el-input type="textarea" :rows="2" placeholder="请输入内容" v-model="textarea"></el-input>
    <pre id="jsonPre" v-html="jsonPre"></pre>
  </div>
</template>
<script>
import configJs from './config'
export default {
  name: 'proxy',
//   computed: {
//     jsonPre() {
//       return this.parse2(configJs)
//     },
//   },
  data() {
    return {
      textarea: JSON.stringify(configJs),
      jsonPre: this.parse2(configJs)
    }
  },
  methods: {
    parse1(str) {
      return JSON.stringify(JSON.parse(str), null, '\t')
    },
    parse2(str) {
      // 设置缩进为2个空格
      str = JSON.stringify(JSON.parse(str), null, 2)
      str = str.replace(/&/g, '&').replace(/</g, '<').replace(/>/g, '>')
      return str.replace(/("(\\u[a-zA-Z0-9]{4}|\\[^u]|[^\\"])*"(\s*:)?|\b(true|false|null)\b|-?\d+(?:\.\d*)?(?:[eE][+\-]?\d+)?)/g, function (match) {
        var cls = 'number'
        if (/^"/.test(match)) {
          if (/:$/.test(match)) {
            cls = 'key'
          } else {
            cls = 'string'
          }
        } else if (/true|false/.test(match)) {
          cls = 'boolean'
        } else if (/null/.test(match)) {
          cls = 'null'
        }
        return '<span class="' + cls + '">' + match + '</span>'
      })
    },
  },
}
</script>
<style>
/* 方法1：设置textarea合适的宽高 */
#jsonTextarea {
  float: left;
  margin-right: 20px;
  width: 40%;
  height: 70vh;
  outline: none;
  padding: 5px;
}

/* 方法2：自定义高亮样式 */
#jsonPre {
  float: left;
  width: 40%;
  height: 70vh;
  outline: 1px solid #ccc;
  padding: 5px;
  overflow: scroll;
}

.string {
  color: green;
}

.number {
  color: darkorange;
}

.boolean {
  color: blue;
}

.null {
  color: magenta;
}

.key {
  color: red;
}
</style>
