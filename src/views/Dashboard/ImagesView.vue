<template>
  <div class="container">
    <form @submit="uploadImage">
    <input id="file" type="file" name="file-to-upload" @change="chooseImage"/>
    <input type="submit" class="btn btn-primary" value="Upload" />
    </form>
    <p>圖片連結:{{imageUrl}}</p>
    <table class="table">
      <thead>
        <tr>
          <th>圖片</th>
          <th>圖片連結</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>圖片</td>
          <td>圖片連結</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  data () {
    return {
      formData: {},
      imageUrl: ''
    }
  },
  methods: {
    chooseImage () {
      const fileInput = document.querySelector('#file')
      const file = fileInput.files[0]
      const formData = new FormData()
      formData.append('file-to-upload', file)
      this.formData = formData
      console.log(formData)
    },
    uploadImage () {
      const url = `${process.env.VUE_APP_API}/api/${process.env.VUE_APP_PATH}/admin/upload`
      this.$http.post(url, this.formData)
        .then((res) => {
          this.imageUrl = res.data.imageUrl
          console.log(res.data.imageUrl)
        })
        .catch((err) => {
          alert(err.data.response)
        })
    }
  }
}
</script>
