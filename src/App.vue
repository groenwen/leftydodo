<template>
  <router-view/>
</template>

<style lang="scss">
@import "./assets/stylesheets/all";
@import url('https://fonts.googleapis.com/css2?family=MuseoModerno:wght@700&family=Noto+Sans+TC:wght@400;600&family=Noto+Serif+TC:wght@400;700&display=swap');

#app {
  font-family: 'Noto Sans TC', Helvetica, Arial, sans-serif;
  letter-spacing: .04em;

}
h2 {
  font-family: 'Noto Serif TC';
  font-weight: 600;
  line-height: 150%;
  letter-spacing: .08em;
  color: $primary;
}
h3 {
  color: $primary;
}
p {
  line-height: 175%;
}

.font-serif {
  font-family: 'Noto Serif TC';
}

section {
  padding-top: 7rem;
  padding-bottom: 7rem;
}
//button
.btn i {
  padding-right: .25rem;
}
.btn-lg i {
  font-size: 150%;
}

// 標題有底線
.accent-title {
  display: inline-block;
  position: relative;
  z-index: 0;
  &::before {
    position: absolute;
    content: '';
    left: -1rem;
    right: -1rem;
    bottom: .25rem;
    height: 1rem;
    background-color: $accent-v;
    border-radius: $border-radius-pill;
    z-index: -1;
  }
}

// 首頁 產品 卡片
.new-card {
  position: relative;
  margin: 0 auto;
  width: 88%;
  height: 23rem;
  border-radius: $border-radius;
  background-image: url('./img/product_01.jpeg');
  background-size: cover;
  background-position:  center;
  box-shadow: 1rem 1rem 0 $light;
  overflow: hidden;
  &-body {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 1.5rem 2rem;
    background-color: rgba($primary, .8);
  }
  & {
    color: $white;
  }
}

// price
.price {
  &-current :nth-child(2) {
    font-size: 150%;
    font-weight: 700;
    padding-left: .25rem;
  }
  &-origin {
    text-decoration: line-through;
  }
}

// head
.backdrop-blur {
  backdrop-filter: blur(.5rem);
}
.head {
  position: relative;
  height: 32rem;
  background-image: url(https://storage.googleapis.com/vue-course-api.appspot.com/groen/1648391384666.png?GoogleAccessId=firebase-adminsdk-zzty7%40vue-course-api.iam.gserviceaccount.com&Expires=1742169600&Signature=BWg%2Bwbvks6BqQe3lAYVWJJci51FmtQ6j9ymuQw6PzrJRTcAoMFRfTc9eXKyxDuPLg%2FkNQ3Bw7V7sXT34n8TKtX5br9lpOQkG%2BFN6Vlnkv4M719DY6IvERYwP2Wu158VMjivf6gGvo8%2BzVX99MIn4k5mzJhC%2B1t7MfRFjbX8vlibZeecbFGBfo%2BPu2dt8SZWXgDjMu5GwukhKp1NP9UUnp0KEyQQu6m3TTVteDwlbs6IrVkiJhamLIGEnQwcnJmO4ikFqbS%2FufS1%2FnzIKpBFh1k61H%2BYKkXB3RFZyFinwxdkWEeSSAY%2FxPxLrrfGS54%2FEaavs1Qry5CLbGqmQnMBiYg%3D%3D);
  background-size: cover;
  background-position:  center;
}

</style>
