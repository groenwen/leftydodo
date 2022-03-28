<template>
  <Header />
  <router-view/>
  <Footer />
</template>

<script>
import Header from '../components/HeaderTemp.vue'
import Footer from '../components/FooterTemp.vue'

export default {
  components: {
    Header,
    Footer
  }
}
</script>
