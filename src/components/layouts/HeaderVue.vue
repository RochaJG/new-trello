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
                <span class="account-user-name">{{trelloUser.fullName}}</span>
            </span>
        </a>
        <div class="dropdown-menu dropdown-menu-right dropdown-menu-animated profile-dropdown ">
            <!-- item-->
            <div class=" dropdown-header noti-title">
                <h6 class="text-overflow m-0">Bem Vindo <span class="text-info">@{{trelloUser.username}}</span>!</h6>
            </div>

            <!-- item-->
            <a @click="trelloLogout()" href class="dropdown-item notify-item">
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
  name: 'HeaderVue',
  data() {
      return {
				trelloUser: {}
      }
  },
  methods: {
      loadTrelloInfo() {
          this.getUserInfo()
      },
      getUserInfo() {
          var vm = this
          this.trelloStats = Trello.authorized()
          if(!this.trelloStats) {
              this.trelloLogin()
          }
          Trello.members.get("me", function (member) {
								vm.trelloUser = member								
            })
      },
      trelloLogin() {				
          Trello.authorize({
                type: 'popup',
                name: 'New Trello',
                interactive: true
            })
      },
      trelloLogout() {
				clearInterval(this.updateDataInterval)
				console.log('Logout');
				
        Trello.deauthorize()
        this.trelloStats = Trello.authorized()
      }
  },
  mounted() {
      this.loadTrelloInfo()
      this.updateDataInterval = setInterval(function () {
            this.loadTrelloInfo()
				}.bind(this), 3000)
  }
}
</script>
