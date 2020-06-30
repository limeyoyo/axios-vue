<template>
  <div class="home">
  </div>
</template>

<script>
// Axios的配置参数
import axios from 'axios'

export default {
  name: 'Axios3-2',
  components: {
  },
  created() {
    axios.create({
        baseURL: 'http://localhost:8080', // 请求的域名，基本地址
        timeout: 1000, // 设置请求的超时时长（ms）
        url: '/data.json', // 请求路径
        method: 'get', // 请求方法
        headers: {
            token: ''
        }, // 设置请求头
        params: {}, // 请求参数拼接在url上
        data: {}, //请求参数放在请求体里
    })

    // Axios全局配置
    axios.defaults.baseURL = "http://localhost:8080"
    axios.defaults.timeout = 1000
    // Axios实例配置
    let instance = axios.create()
    instance.defaults.timeout = 3000
    // Axios请求配置
    instance.get('/data.json', {
        timeout: 5000
    })

    // 优先级：从低到高

    // 实际开发
    // 由两种请求接口
    // http://localhost:9000
    // http://localhost:9001
    let instance9000 = axios.create({
        baseURL: 'http://localhost:9000',
        timeout: 1000
    })
    let instance9001 = axios.create({
        baseURL: 'http://localhost:9001',
        timeout: 3000
    })
    // baseURL,timeout,url,method,params
    instance9000.get('/contactList', {
        params: {}
    }).then( res => {
        console.log(res)
    })
    // baseURL,timeout:5000,url,method
    instance9001.get('/orderList', {
        timeout: 5000
    }).then( res => {
        console.log(res)
    })
  }
}
</script>
