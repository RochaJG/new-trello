<template>
  <div class="wrapper">
    <header>
      
    </header>

    <nav class="left-side-menu">
      <div class="slimscroll-menu">
        <!-- LOGO -->
        <a href="index.html" class="logo text-center">
            <span class="logo-lg">
                <img src="assets/images/logo.png" alt="" height="16">
            </span>
            <span class="logo-sm">
                <img src="assets/images/logo_sm.png" alt="" height="16">
            </span>
        </a>

        <ul class="metismenu side-nav">
          <li class="side-nav-title side-nav-item">Menu</li>
          <li class="side-nav-item">
            <router-link class="side-nav-link" to="/">
              <i class="mdi mdi-home"></i>
              <span> Início </span>
            </router-link>
          </li>
        </ul>
      </div>
    </nav>

    <main class="content-page">
      <router-view></router-view>
    </main>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>
