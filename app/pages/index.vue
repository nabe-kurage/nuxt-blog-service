<template>
  <section class="container">
    <el-card>
      <div slot="header">
        <span>ログイン</span>
      </div>
      <form action="">
        <div class="form-content">
          <span>ユーザー ID</span>
          <el-input placeholder="" v-model="formData.id"></el-input>
        </div>
        <div class="form-content">
          <el-checkbox v-model="isCreateMode">アカウントを作成する</el-checkbox>
        </div>
        <div class="text-right">
          <el-button type="primary" @click="hundleClickSubmit">{{buttonText}}</el-button>
        </div>
      </form>
    </el-card>
  </section>
</template>

<script>
import {mapGetters, mapActions} from 'vuex'
import Cookie from 'universal-cookie'

export default {
  asyncData({redirect, store}) {
    if(store.getters['user']){
      redirect('/posts/')
    }
    return {
      isCreateMode: false,
      formData: {
        id:''
      }
    }
  },
  computed: {
    buttonText() {
      return this.isCreateMode? '新規登録': 'ログイン'
    },
    ...mapGetters(['user'])
  },
  methods: {
    async hundleClickSubmit() {
      const cookies = new Cookies()
      if(this.isCreateMode) {
        try{
          await this.register({...this.formData})
          this.$notify({
            type: 'success',
            title: 'アカウント作成完了',
            message: '登録しました',
            position: 'bottom-right',
            duration: 1000
          })
          cookies.set('user, JSON.stringify(this.user')
          this.$router.push('/posts/')
        } catch (e) {
          this.$notify.error({
            title: 'アカウント作成失敗',
            message: '登録できませんでした',
            position: 'bottom-right',
            duration: 1000
          })
        }
      } else {
        try{
          await this.register({...this.formData})
          this.$notify({
            type: 'success',
            title: 'ログイン成功',
            message: 'ログインしました',
            position: 'bottom-right',
            duration: 1000
          })
          cookies.set('user, JSON.stringify(this.user')
          this.$router.push('/posts/')
        } catch (e) {
          this.$notify.error({
            title: 'ログイン作成失敗',
            message: 'ログインできませんでした',
            position: 'bottom-right',
            duration: 1000
          })
        }
      }
    },
    ...mapActions(['login', 'register'])
  }
}
</script>

<style>
.form-content {
  margin: 16px 0;
}
</style>
