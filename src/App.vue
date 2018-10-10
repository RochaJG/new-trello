<template>
  <div>
    <span class="wrapper">
      <nav-bar>
        <li class="side-nav-title side-nav-item">Menu</li>
        <menu-link goto="/" title="Início" icon="home" />
        <menu-link goto="/boards" title="Quadros" icon="developer-board" />
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

    <right-bar></right-bar>
  </div>
</template>

<script>
import NavBar from '@/components/layouts/NavBar'
import RightBar from '@/components/layouts/RightBar'
import HeaderVue from '@/components/layouts/HeaderVue'
import MenuLink from '@/components/layouts/MenuLink'

export default {
  name: 'app',
  components: {
    NavBar,
    RightBar,
    HeaderVue,
    MenuLink,
  },
}
</script>
