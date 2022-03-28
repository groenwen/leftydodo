<template>
  <div>
    <h1>後台首頁</h1>
    <button type="button" class="btn btn-primary" @click="signout()">登出</button>
    <nav>
      <router-link to="/admin/products">產品列表</router-link> |
      <router-link to="/admin/images">上傳圖片</router-link> |
    </nav>
    <router-view />
  </div>
</template>
<script>
export default {
  data () {
    return {

    }
  },
  methods: {
    checkAdmin () {
      // 取出 token
      const token = document.cookie.replace(/(?:(?:^|.*;\s*)groenToken\s*=\s*([^;]*).*$)|^.*$/, '$1')
      const url = `${process.env.VUE_APP_API}/api/user/check`

      // 驗證使用者
      this.$http.defaults.headers.common.Authorization = token

      if (token) {
        this.$http.post(url)
          .then((res) => {
            // 驗證成功
          })
          .catch((err) => {
            // 驗證錯誤 回到登入頁面
            alert(err.data.message)
            this.$router.push('/login')
          })
      } else {
        alert('尚未登入後台')
        this.$router.push('/login')
      }
    },
    signout () {
      document.cookie = 'groenToken=;expires=;'
      alert('已登出後台')
      this.$router.push('/login')
    }
  },
  mounted () {
    this.checkAdmin()
  }
}
</script>
