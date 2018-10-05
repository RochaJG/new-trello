<template>
  <nav class="left-side-menu">
      <div class="slimscroll-menu">
        <!-- LOGO -->
        <router-link to="/" class="logo text-center">
            <span class="logo-lg">
                <img src="/static/img/logo.png" alt="" height="44">
            </span>
            <span class="logo-sm">
                <img src="/static/img/logo_sm.png" alt="" height="16">
            </span>
        </router-link>

        <ul class="metismenu side-nav">
          <slot></slot>
        </ul>
      </div>
    </nav>
</template>

<script>
export default {
  name: 'NavBar',
}
</script>
