<template>
  <router-view/>
</template>

<style lang="scss">
@import "./assets/stylesheets/all";
@import url('https://fonts.googleapis.com/css2?family=MuseoModerno:wght@700&family=Noto+Sans+TC:wght@400;600&family=Noto+Serif+TC:wght@400;700&display=swap');

@mixin accent-line($color) {
  height: 1rem;
  background-color: $color;
  border-radius: $border-radius-pill;
}

#app {
  font-family: 'Noto Sans TC', Helvetica, Arial, sans-serif;
  letter-spacing: .1em;
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
.btn-secondary {
  color: $white;
}

.lefty-shadow {
  box-shadow: 0 0 .5rem rgba(#000, .1);
}

// 標題有底線
.accent-line {
  @include accent-line($accent);
}
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
    z-index: -1;
    @include accent-line($accent-v);
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
  text-align: right;
  &-current :nth-child(2) {
    font-size: 150%;
    font-weight: 700;
    padding-left: .25rem;
  }
  &-origin {
    text-decoration: line-through;
    letter-spacing: 0;
  }
}

// head
.head {
  position: relative;
  height: 28rem;
  background: linear-gradient(rgba(#000, .2), rgba(#000, .2)), linear-gradient(rgba($light-v, .25), rgba($light-v, .25)), url('./img/bn_01.jpg') center / cover;
  z-index: -1;
}
.backdrop-blur {
  backdrop-filter: blur(.25rem);
}
.bg-flag {
  background: url('./img/flag.png') center top no-repeat;
}

</style>
