<template>
  <div class="home">
    <!-- <van-button type="default">默认按钮</van-button> -->
      <van-contact-list
      :list="list"
      @add="onAdd"
      @edit="onEdit"
    />
    <van-popup v-model="showEdit" position="bottom">
      <van-contact-edit
        :contact-info="editingContact"
        :is-edit="isEdit"
        @save="onSave"
        @delete="onDelete"
      />
   </van-popup>
  </div>
</template>

<script>
import axios from 'axios'
// import { Button } from 'vant'
import { ContactList, ContactEdit, Popup } from 'vant';
import { Toast } from 'vant'
export default {
  name: 'contactList',
  components: {
      // [Button.name]:Button
      [ContactList.name]:ContactList,
      [ContactEdit.name]:ContactEdit,
      [Popup.name]:Popup
  },
  data() {
    return {
      list: [],
      instance: null, // axios实例
      showEdit: false, // 编辑弹窗的显示与隐藏
      editingContact: {}, //正在编辑的联系人数据
      isEdit: false, // 新建与编辑
    }
  },
  created() {
    this.instance = axios.create({
      baseURL: 'http://localhost:9000/api',
      timeout: 1000
    })
    this.getList()
  },
  methods: {
    getList() {
      this.instance.get('/contactList').then(res => {
        console.log(res);
        this.list = res.data.data
      }).catch( err => {
        console.log(err)
        Toast('请求失败，请稍后重试')
      })
    },
    onAdd() {
      this.showEdit = true
      this.isEdit = false
    },
    onEdit(info) {
      this.showEdit = true
      this.isEdit = true
      this.editingContact = info
    },
    onSave(info) {
      console.log(info, 'info')
      if (this.isEdit) {
        // 编辑保存
        this.instance.put('/contact/edit', info).then( res => {
          if (res.data.code === 200){
            Toast('编辑成功')
            this.showEdit = false
            this.getList()
          }
        }).catch( () => {
          Toast('请求失败，请稍后重试')
        })
      } else {
        // 新建保存
        this.instance.post('/contact/new/json', info).then( res => {
          if (res.data.code === 200){
            Toast('新建成功')
            this.showEdit = false
            this.getList()
          }
        }).catch( () => {
          Toast('请求失败，请稍后重试')
        })
      }
    },
    onDelete(info) {
      this.instance.delete('/contact', {
        params: {
          id: info.id
        }
      }).then( res => {
          if (res.data.code === 200){
            Toast('删除成功')
            this.showEdit = false
            this.getList()
          }
        }).catch( () => {
          Toast('请求失败，请稍后重试')
        })
    }
  }
}
</script>
<style lang="less" scoped>
.van-contact-list__add{
  z-index: 0;
}
.van-popup{
  height: 100%;
}
</style>
