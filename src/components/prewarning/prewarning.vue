<template>
  <div>
    <span>预警监控</span>
    <vue-loading v-show="loading" type="bars" color="#d9544e" :size="{ width: '50px', height: '50px' }"></vue-loading>
  </div>
</template>

<script>
export default {
  name: 'prewarning',
  data () {
    return {
      loading: false,
      formData: {
        name: '',
        passwd: ''
      }
    }
  },
  methods: {
    submit () {
      this.loading = true
      provider.login(this, this.formData).then(data => {
      // provider.login(this, {UserPo: this.formData}).then(data => {
        this.loading = false
        if (data.body.header.status === 1) {
          localStorage.setItem('token', data.body.body.token)
          console.log(localStorage.getItem('token'))
          localStorage.setItem('userInfo', JSON.stringify(data.body.userInfo))
          this.$router.push({path: '/prewarning'})
        } else {
          // alert(data.body.errorMessage)
          alert(data.body.body.errorMessage)
        }
      })
    }
  }
}
</script>

<style lang="stylus">
font-size = 12px   //定义变量
@import '../../css/base.styl'
.input-w
  line-height 40px
  @extends .clearfix
  .label
    float left
    width 120px
  .input-item
    padding-left 10px
    height 32px
    width 320px
    border 1px solid #ddd
    border-radius 5px
</style>
