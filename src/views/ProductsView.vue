<template>
  <div class="head">
    <div class="backdrop-blur bg-flag d-flex justify-content-center align-items-center h-100">
      <div class="text-center">
        <h5 class="text-accent font-serif">- All Products -</h5>
        <h1 class="text-white font-serif fw-bold my-4">給寶寶最好的</h1>
        <div class="accent-line w-75 mx-auto"></div>
      </div>
    </div>
  </div>
  <div class="main">
    <div class="container">
      <ul class="category">
        <li>
          <a href="" class="btn btn-secondary text-white">ALL</a>
        </li>
        <li>
          <a href="" class="btn btn-white text-secondary">圍兜兜・口水巾</a>
        </li>
        <li>
          <a href="" class="btn btn-white text-secondary">左手出品</a>
        </li>
        <li>
          <a href="" class="btn btn-white text-secondary">包屁衣</a>
        </li>
        <li>
          <a href="" class="btn btn-white text-secondary">豆豆毯</a>
        </li>
        <li>
          <a href="" class="btn btn-white text-secondary">感統玩具</a>
        </li>
      </ul>
      <div class="text-center mb-6">
        <img class="mb-3" src="../img/tree.png" height="48" alt="">
        <h2>圍兜兜・口水巾</h2>
      </div>
      <div class="row row-cols-lg-4 gy-4">
        <div class="col" v-for="item in products" :key="item.id">
          <div class="card product lefty-shadow">
            <div class="card-img" :style="{ backgroundImage: 'url(' + item.imageUrl + ')' }" style="height: 200px; background-size: cover; background-position: center;">
            </div>
            <div class="card-body">
              <div class="d-flex justify-content-between">
                <h5 class="card-title text-primary">{{ item.title }}</h5>
                <div class="price">
                  <div class="price-current text-secondary-v"><span>NT$</span><span>{{ item.price }}</span></div>
                  <div class="price-origin">NT$ <span>{{ item.origin_price }}</span></div>
                </div>
              </div>
              <div class="text-end pt-4 pb-2">
                <a href="" class="btn btn-outline-primary">加入購物車</a>
              </div>
            </div>
          </div>
        </div>
      </div>
      <Pagination :pages="pagination" @emit-pages="getProducts"></Pagination>
      <v-loading :active="isLoading" :loader="'dots'"></v-loading>
    </div>
  </div>
</template>

<style lang="scss">
@import "../assets/stylesheets/all";
.category {
  display: flex;
  margin: 0 auto 1rem;
  padding: 1rem 3rem;
  width: fit-content;
  transform: translateY(-50%);
  list-style: none;
  border-radius: 1.5rem;
  border: 1px solid $light;
  background-color: $light-v;
  box-shadow: 0 0 .5rem rgba(#000, .1);
  li {
    padding-left: .25rem;
    padding-right: .25rem;
  }
}
.card.product {
  .card-img {
    border-bottom-left-radius: 0;
    border-bottom-right-radius: 0;
  }
  .card-title {
    padding-right: 2rem;
  }
}

</style>
<script>
import Pagination from '../components/PaginationTemp.vue'

export default {
  data () {
    return {
      isLoading: false,
      products: [],
      productItem: {},
      pagination: {}
    }
  },
  components: {
    Pagination
  },
  methods: {
    getProducts (page = 1) {
      this.isLoading = true
      this.$http
        .get(`${process.env.VUE_APP_API}/api/${process.env.VUE_APP_PATH}/products?page=${page}`)
        .then((res) => {
          this.isLoading = false
          this.products = res.data.products
          this.pagination = res.data.pagination
        })
    },
    openModal (item) {
      this.$refs.callModal.innerOpenModal()
      this.productItem = item
    },
    hideModal () {
      this.$refs.callModal.innerhideModal()
    },
    // 加入購物車
    addToCart (productId, qty = 1) {
      const url = `${process.env.VUE_APP_API}/api/${process.env.VUE_APP_PATH}/cart`
      const data = { product_id: productId, qty }
      this.isLoading = true
      this.$http
        .post(url, { data })
        .then((res) => {
          this.isLoading = false
          this.hideModal()
          alert(res.data.message)
        }).catch((err) => {
          alert(err.data)
          this.isLoading = false
        })
    }
  },
  mounted () {
    this.getProducts()
  }
}
</script>
