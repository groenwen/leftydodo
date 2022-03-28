<template>
  <div class="container">
    <h2>產品列表</h2>
    <div class="text-end mt-4">
      <!-- 建立新產品  isNew = 'new' -->
      <button
        class="btn btn-primary"
        data-bs-toggle="myModal"
        data-bs-target="#exampleModal"
        @click="openModal('new')"
      >
        建立新的產品
      </button>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>分類</th>
          <th></th>
          <th>產品名稱</th>
          <th>原價</th>
          <th>售價</th>
          <th>是否啟用</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in products" :key="item.id">
          <td>{{ item.category }}</td>
          <td><img :src="item.imageUrl" height="100" /></td>
          <td>{{ item.title }}</td>
          <td>{{ item.origin_price }}</td>
          <td>{{ item.price }}</td>
          <td>
            <!-- 切換 啟用 / 未啟用 -->
            <div
              class="form-check form-switch"
              @click="
                item.is_enabled ? (item.is_enabled = 0) : (item.is_enabled = 1);
                productItem = item;
                getProduct(item.id)
              "
            >
              <input
                class="form-check-input"
                type="checkbox"
                role="switch"
                id="flexSwitchCheckDefault"
                :checked="item.is_enabled"
              />
              <label
                class="form-check-label"
                for="flexSwitchCheckDefault"
                v-if="item.is_enabled"
                >啟用</label
              >
              <label
                class="form-check-label"
                for="flexSwitchCheckDefault"
                v-else
                >未啟用</label
              >
            </div>
          </td>
          <td>
            <div class="btn-group">
              <!-- 編輯產品  isNew = 'edit' ，並帶入該產品資訊 -->
              <button
                type="button"
                class="btn btn-outline-primary btn-sm"
                @click="openModal('edit', item)"
              >
                編輯
              </button>
              <!-- 刪除產品  isNew = 'delete' ，並帶入該產品資訊 -->
              <button
                type="button"
                class="btn btn-outline-danger btn-sm"
                @click="openModal('delete', item)"
              >
                刪除
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
    <Pagination :pages="pagination" @emit-pages="getProducts" />
    <ProductModal ref="callModal" :productItem="productItem" :isNew="isNew" />
    <DelProductModal ref="callDelModal" :productItem="productItem" />
  </div>
</template>
<script>
import Pagination from '../../components/PaginationTemp.vue'
import ProductModal from '../../components/ProductModal.vue'
import DelProductModal from '../../components/DelProductModal.vue'

export default {
  data () {
    return {
      api: {
        api: process.env.VUE_APP_API,
        path: process.env.VUE_APP_PATH
      },
      // 共用 modal 判斷點擊 新增/編輯
      isNew: false,
      // 儲存 單一產品資訊
      productItem: {
        imagesUrl: []
      },
      products: '',
      pagination: {}
    }
  },
  components: {
    Pagination,
    ProductModal,
    DelProductModal
  },
  methods: {
    getProducts (page = 1) {
      const url = `${this.api.api}/api/${this.api.path}/admin/products?page=${page}`
      this.$http
        .get(url)
        .then((res) => {
          this.products = res.data.products
          this.pagination = res.data.pagination
        })
        .catch((err) => {
          alert(err.data.message)
        })
    },
    getProduct (id) {
      const url = `${this.api.api}/api/${this.api.path}/admin/product/${id}`

      this.$http
        .put(url, { data: this.productItem })
        .then((res) => {
          alert(res.data.message)
          // 關閉 modal
          this.$refs.callModal.innerhideModal()
        })
        .catch((err) => {
          alert(err.data.message)
        })
    },
    // modal 控制
    openModal (isNew, item) {
      // 新增產品
      if (isNew === 'new') {
        // 建立產品
        console.log('new')
        this.productItem = {
          imagesUrl: []
        }
        this.isNew = true
        this.$refs.callModal.innerOpenModal()
      } else if (isNew === 'edit') {
        console.log('edit')
        // 編輯產品
        // 帶入產品資訊
        this.productItem = { ...item }

        this.isNew = false
        this.$refs.callModal.innerOpenModal()
      } else if (isNew === 'delete') {
        // 刪除產品
        this.productItem = { ...item }
        this.$refs.callDelModal.innerOpenModal()
      }
    },
    hideModal () {
      this.$refs.callModal.innerhideModal()
    }
  },
  mounted () {
    this.getProducts()
  }
}
</script>
