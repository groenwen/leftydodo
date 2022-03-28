<template>
  <div
    id="productModal"
    ref="productModal"
    class="modal fade"
    tabindex="-1"
    aria-labelledby="productModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-xl modal-dialog-scrollable">
      <div class="modal-content border-0">
        <div class="modal-header bg-dark text-white">
          <h5 id="productModalLabel" class="modal-title">
            <span v-if="isNew">新增產品</span>
            <span v-else>編輯產品</span>
          </h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <div class="row">
            <div class="col-sm-4">
              <div class="mb-2">
                <div class="mb-3">
                  <label for="imageUrl" class="form-label">主要圖片</label>
                  <input
                    type="text"
                    class="form-control"
                    placeholder="請輸入圖片連結"
                    v-model="newProductItem.imageUrl"
                  />
                </div>
                <img class="img-fluid" :src="newProductItem.imageUrl" alt="" />
              </div>
              <h3 class="mt-5 mb-3">多圖新增</h3>

              <!-- 判斷是否為 陣列 ， 1-編輯產品 0-建立新產品 -->
              <div v-if="Array.isArray(newProductItem.imagesUrl)">
                <!-- 顯示 既有的圖片 -->
                <div
                  class="mb-2"
                  v-for="(img, key) in newProductItem.imagesUrl"
                  :key="key"
                >
                  <div class="mb-3">
                    <label for="imageUrl" class="form-label">圖片網址</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="newProductItem.imagesUrl[key]"
                    />
                  </div>
                  <img class="img-fluid" :src="img" alt="" />
                  <!-- 刪除 單一圖片  按鈕 -->
                  <div class="mt-2 mb-5">
                    <button
                      class="btn btn-outline-danger btn-sm d-block w-100"
                      @click="delImage(key)"
                    >
                      刪除圖片
                    </button>
                  </div>
                </div>
                <!-- 新增圖片 -->
                <div class="mt-5">
                  <button
                    class="btn btn-outline-primary btn-sm d-block w-100"
                    @click="newProductItem.imagesUrl.push('')"
                  >
                    新增圖片
                  </button>
                </div>
              </div>
              <!-- 新增圖片 -->
              <div v-else>
                <button
                  class="btn btn-outline-primary btn-sm d-block w-100"
                  @click="createImages"
                >
                  新增圖片
                </button>
              </div>
            </div>
            <div class="col-sm-8">
              <div class="mb-3">
                <label for="title" class="form-label">標題</label>
                <input
                  id="title"
                  type="text"
                  class="form-control"
                  placeholder="請輸入標題"
                  v-model="newProductItem.title"
                />
              </div>

              <div class="row">
                <div class="mb-3 col-md-6">
                  <label for="category" class="form-label">分類</label>
                  <input
                    id="category"
                    type="text"
                    class="form-control"
                    placeholder="請輸入分類"
                    v-model="newProductItem.category"
                  />
                </div>
                <div class="mb-3 col-md-6">
                  <label for="price" class="form-label">單位</label>
                  <input
                    id="unit"
                    type="text"
                    class="form-control"
                    placeholder="請輸入單位"
                    v-model="newProductItem.unit"
                  />
                </div>
              </div>

              <div class="row">
                <div class="mb-3 col-md-6">
                  <label for="origin_price" class="form-label">原價</label>
                  <!-- 若 單純使用 v-model 而非 v-model.number 會顯示 型別錯誤 (轉為 number) -->
                  <input
                    id="origin_price"
                    type="number"
                    min="0"
                    class="form-control"
                    placeholder="請輸入原價"
                    v-model.number="newProductItem.origin_price"
                  />
                </div>
                <div class="mb-3 col-md-6">
                  <label for="price" class="form-label">售價</label>
                  <!-- 若 單純使用 v-model 而非 v-model.number 會顯示 型別錯誤 (轉為 number) -->
                  <input
                    id="price"
                    type="number"
                    min="0"
                    class="form-control"
                    placeholder="請輸入售價"
                    v-model.number="newProductItem.price"
                  />
                </div>
              </div>
              <hr />

              <div class="mb-3">
                <label for="description" class="form-label">產品描述</label>
                <textarea
                  id="description"
                  type="text"
                  class="form-control"
                  placeholder="請輸入產品描述"
                  v-model="newProductItem.description"
                >
                </textarea>
              </div>
              <div class="mb-3">
                <label for="content" class="form-label">說明內容</label>
                <textarea
                  id="description"
                  type="text"
                  class="form-control"
                  placeholder="請輸入說明內容"
                  v-model="newProductItem.content"
                >
                </textarea>
              </div>
              <div class="mb-3">
                <div class="form-check">
                  <input
                    id="is_enabled"
                    class="form-check-input"
                    type="checkbox"
                    :true-value="1"
                    :false-value="0"
                    v-model="newProductItem.is_enabled"
                  />
                  <label class="form-check-label" for="is_enabled"
                    >是否啟用</label
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-outline-secondary"
            data-bs-dismiss="modal"
          >
            取消
          </button>
          <!-- 更新產品資訊 -->
          <button type="button" class="btn btn-primary" @click="getProduct">
            確認
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Modal from 'bootstrap/js/dist/modal'

export default {
  props: ['productItem', 'isNew'],
  data () {
    return {
      thisModal: '',
      newProductItem: {},
      newIsNew: ''
    }
  },
  watch: {
    productItem () {
      this.newProductItem = this.productItem
    },
    isNew () {
      this.newIsNew = this.isNew
    }
  },
  methods: {
    innerOpenModal () {
      this.thisModal.show()
    },
    innerhideModal () {
      this.thisModal.hide()
    }
  },
  mounted () {
    this.thisModal = new Modal(this.$refs.productModal)
    this.newProductItem = this.productItem
    this.newIsNew = this.isNew
    console.log(this.productItem)
  }
}
</script>
