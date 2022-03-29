<template>
  <nav class="my-6" aria-label="Page navigation example">
    <ul class="pagination justify-content-center">
      <li class="page-item" :class="{ disabled: !pages.has_pre }">
        <a
          class="page-link"
          href="#"
          aria-label="Previous"
          @click.prevent="emitPages(pages.current_page - 1)"
        >
          <span aria-hidden="true"><i class="bi bi-chevron-left"></i></span>
        </a>
      </li>
      <li
        class="page-item"
        v-for="item in pages.total_pages"
        :key="item"
        :class="{ active: pages.current_page === item }"
      >
        <a class="page-link" href="#" @click.prevent="emitPages(item)">{{
          item
        }}</a>
      </li>
      <li class="page-item" :class="{ disabled: !pages.has_next }">
        <a
          class="page-link"
          href="#"
          aria-label="Next"
          @click.prevent="emitPages(pages.current_page + 1)"
        >
          <span aria-hidden="true"><i class="bi bi-chevron-right"></i></span>
        </a>
      </li>
    </ul>
  </nav>
</template>

<style lang="scss">
.page-item {
  padding-left: .25rem;
  padding-right: .25rem;
}
.page-link{
  border-radius: 50rem;
  line-height: 1;
}
</style>

<script>
export default {
  props: ['pages'],
  methods: {
    emitPages (item) {
      this.$emit('emit-pages', item)
    }
  }
}
</script>
