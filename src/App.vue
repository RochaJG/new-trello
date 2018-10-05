<template>
  <span class="wrapper">
    <nav-bar>
      <li class="side-nav-title side-nav-item">Menu</li>
      <li class="side-nav-item">
        <router-link class="side-nav-link" to="/">
          <i class="mdi mdi-home"></i>
          <span> Início </span>
        </router-link>
      </li>
    </nav-bar>

    <main class="content-page">
      <div class="content">
        <header-vue/>
        <div class="container-fluid">
          <router-view></router-view>
        </div>
      </div>
    </main>
  </span>
</template>

<script>
import NavBar from '@/components/layouts/NavBar'
import HeaderVue from '@/components/layouts/HeaderVue'

export default {
  name: 'app',
  components: {
    NavBar,
    HeaderVue
  }
}
</script>
