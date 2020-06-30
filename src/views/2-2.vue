<template>
  <div class="home">

  </div>
</template>

<script>

/**
 * Axios的请求方法：get,post,put,patch,delete
 * get：获取数据
 * post：提交数据（表单提交/文件上传）
 * put：更新数据（将所有的数据都推送到后端）
 * patch：更新数据（只将修改的数据推送到后端）
 * delete：删除数据
 */
import axios from 'axios'

export default {
  name: 'Axios2-2',
  components: {
  },
  created() {
    // http://localhost:8080/data.json?id=22
    axios.get('/data.json', {
        params: {
            id: 22
        }
    }).then( res => {
      console.log(res);
    }),
    axios({
        method: 'get',
        url: '/data.json',
        params: {
            id: 22
        }
    }).then( res => {
      console.log(res)
    })
    // form-data 表单提交(图片上传，文件上传)
    // application/json Content-Type: application/json;charset=UTF-8
    axios.post('/post', { id: 22}).then( res => {
        console.log(res)
    })
    axios({
        method: 'post',
        url: '/post',
        data: {id: 22}
    }).then( res => {
        console.log(res)
    })
    // form-data请求
    let formData = new FormData()
    let data = { id: 12}
    for ( let key in data ) {
        formData.append(key, data[key])
    }
    // Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryoLUGC1wCUopF5GLW
    axios.post('/post', formData).then( res => {
        console.log(res)
    })

    axios.put('/put', data).then( res => {
        console.log(res)
    })
    axios.patch('/patch', data).then( res => {
        console.log(res)
    })

    axios.delete('/delete', {
        params: {
            id: 12
        }
    }).then( res => {
        console.log(res)
    })

    axios.delete('/delete', {
        data: {
            id: 12
        }
    }).then( res => {
        console.log(res)
    })
  }
}
</script>
