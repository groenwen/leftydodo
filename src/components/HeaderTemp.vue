<template>
  <div class="container">
    <nav class="navbar navbar-expand-lg sticky-top">
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand text-primary d-flex">
      <img src="../img/logo.svg" alt="">
      </router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavDropdown"
        aria-controls="navbarNavDropdown"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item">
            <router-link to="/products" class="nav-link">關於左撇子</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/products" class="nav-link">所有產品</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/login" class="nav-link">購物須知</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/login" class="nav-link">後台登入</router-link>
          </li>
          <li>
            <router-link to="/cart" class="nav-link nav-link-cart bg-light rounded-circle text-primary p-0 text-center"><i class="bi bi-bag" style="font-size: 1.5rem"></i></router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  </div>
</template>
<style lang="scss">
  .nav-link-cart {
    width: 2.5rem;
    height: 2.5rem;
  }
</style>
