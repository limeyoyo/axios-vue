<template>
  <div class="home">
  </div>
</template>

<script>
// 错误处理：请求错误时进行的处理
import axios from 'axios'

export default {
  name: 'Axios3-4',
  components: {
  },
  created() {
    // 请求拦截器
    axios.interceptors.request.use( config => {
        return config
    }, err => {
        return Promise.reject(err) // 常见的请求错误：404接口没有找到，401请求超时
    })
    // 响应拦截器
    axios.interceptors.response.user( res => {
        console.log(res)
    }, err => {
        console.log(err)
    })
    axios.get('/data.json').then(res => {
      console.log(res);
    }).catch( err => {
        console.log(err)
    })

    // 例：实际开发过程中，一般添加统一的错误处理
    let instance = axios.create({})
    instance.interceptors.request( config => {
        return config
    }, err => {
        // 请求错误：一般http状态码以4开头
        return Promise.reject(err)
    })
    instance.interceptors.response( res => {
        return res
    }, err => {
        // 响应错误：一般http状态码以5开头，500系统错误，502系统重启
        return Promise.reject(err)
    })
  }
}
</script>
