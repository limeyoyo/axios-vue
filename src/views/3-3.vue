<template>
  <div class="home">
  </div>
</template>

<script>
// 拦截器：在请求或响应被处理前拦截它们
// 请求拦截器，响应拦截器
import axios from 'axios'

export default {
  name: 'Axios3-3',
  components: {
  },
  created() {
    // 请求拦截器
    axios.interceptors.request.use( config => {
        // 发送请求前
        return config
    }, err => {
        // 请求错误时
        return Promise.reject(err)
    })

    // 响应拦截器
    axios.interceptors.response.use( res => {
        // 请求成功对响应数据做处理
        return res
    }, err => {
        // 响应错误
        return Promise.reject(err)
    })

    // 取消拦截器
    let interceptors = axios.interceptors.request.use( config => {
        config.headers = {
            auth: true
        }
        return config
    })
    axios.interceptors.request.eject(interceptors)

    // 例：登录状态（token:''） 需要登陆的接口
    let instance = axios.create({})
    instance.interceptors.request.use( config => {
        config.headers.token = '' // 实际开发中headers不止token一个参数，不能直接赋对象
        return config
    })

    // 移动端开发
    let instance_phone = axios.create({})
    instance_phone.interceptors.request.use( config => {
        // show modal
        return config
    })
    instance_phone.interceptors.response.use( res => {
        // hide modal
        return res
    })

  }
}
</script>
