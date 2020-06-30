<template>
  <div class="home">
  </div>
</template>

<script>
// Axios实例
// 后端接口地址有多个，并且超时时长不一样
import axios from 'axios'

export default {
  name: 'Axios3-1',
  components: {
  },
  created() {
      // 超时时长：在发起http请求的时候，服务器端长时间没有返回数据，接口报超时401错误，超时时常一般是由后端定义
      let instance = axios.create({
          baseURL: 'http://localhose:8080',
          timeout: 1000  // 设置超时时长
      })
      instance.get('/data.json').then( res => {
          console.log(res)
      })
  }
}
</script>
