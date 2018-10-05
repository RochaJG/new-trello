<template>
  <div class="navbar-custom">
    <ul class="list-unstyled topbar-right-menu float-right mb-0">
      <li class="dropdown notification-list">
        <a class="nav-link dropdown-toggle nav-user arrow-none mr-0" data-toggle="dropdown" href="index.html#" role="button" aria-haspopup="false"
            aria-expanded="false">
            <span class="account-user-avatar"> 
                <img src="/static/img/profile.png" alt="user-image" class="rounded-circle">
            </span>
            <span>
                <span class="account-user-name">Dominic Keller</span>
                <span class="account-position">Founder</span>
            </span>
        </a>
        <div class="dropdown-menu dropdown-menu-right dropdown-menu-animated profile-dropdown ">
            <!-- item-->
            <div class=" dropdown-header noti-title">
                <h6 class="text-overflow m-0">Welcome !</h6>
            </div>

            <!-- item-->
            <a href="javascript:void(0);" class="dropdown-item notify-item">
                <i class="mdi mdi-account-circle"></i>
                <span>My Account</span>
            </a>

            <!-- item-->
            <a href="javascript:void(0);" class="dropdown-item notify-item">
                <i class="mdi mdi-account-settings-variant"></i>
                <span>Settings</span>
            </a>

            <!-- item-->
            <a href="javascript:void(0);" class="dropdown-item notify-item">
                <i class="mdi mdi-lifebuoy"></i>
                <span>Support</span>
            </a>

            <!-- item-->
            <a href="javascript:void(0);" class="dropdown-item notify-item">
                <i class="mdi mdi-lock-outline"></i>
                <span>Lock Screen</span>
            </a>

            <!-- item-->
            <a href="javascript:void(0);" class="dropdown-item notify-item">
                <i class="mdi mdi-logout"></i>
                <span>Logout</span>
            </a>

        </div>
      </li>
    </ul>
    <button class="button-menu-mobile open-left disable-btn">
      <i class="mdi mdi-menu"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: 'HeaderVue'
}
</script>
