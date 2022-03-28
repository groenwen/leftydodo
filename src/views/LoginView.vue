<template>
  <div class="container">
    <h1>後台登入</h1>
    <div class="row justify-content-center">
      <div class="col-6">
        <v-form v-slot="{errors}" @submit="login">
          <div class="mb-3">
            <label for="email" class="form-label"
              >Email address</label
            >
            <v-field
              type="email"
              name="email"
              id="email"
              class="form-control"
              :class="{ 'is-invalid': errors['email'] }"
              placeholder="請輸入 Email" rules="email|required"
              v-model="user.username">
              </v-field>
            <error-message name="email" class="invalid-feedback"></error-message>
            <div id="emailHelp" class="form-text">
              We'll never share your email with anyone else.
            </div>
          </div>
          <div class="mb-3">
            <label for="password" class="form-label"
              >Password</label
            >
            <v-field
              type="password"
              name="password"
              id="password"
              class="form-control"
              :class="{ 'is-invalid': errors['password']}"
              placeholder="請輸入密碼" rules="required"
              v-model="user.password"
            ></v-field>
          </div>
          <button type="submit" class="btn btn-primary">Submit</button>
        </v-form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      user: {
        username: 'yuwen7005@gmail.com',
        password: ''
      }
    }
  },
  methods: {
    login () {
      const url = `${process.env.VUE_APP_API}/admin/signin`
      this.$http.post(url, this.user)
        .then((res) => {
          // 登入成功
          const { token, expired } = res.data
          document.cookie = `groenToken=${token};expires=${new Date(expired)};path=/`
          this.$router.push('/admin')
        })
        .catch((err) => {
          alert(err.data.message)
        })
    }
  }
}
</script>
