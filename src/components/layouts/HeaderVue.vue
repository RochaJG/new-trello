<template>
	<div class="navbar-custom">
	<ul class="list-unstyled topbar-right-menu float-right mb-0">
		<li class="dropdown notification-list">
			<a class="nav-link dropdown-toggle arrow-none" data-toggle="dropdown" href role="button" aria-haspopup="false" aria-expanded="false" @click="hadNotif = false">
				<i class="dripicons-bell noti-icon"></i>
				<span class="noti-icon-badge" v-show="hadNotif"></span>
			</a>
			<div class="dropdown-menu dropdown-menu-right dropdown-menu-animated dropdown-lg">

				<!-- item-->
				<div class="dropdown-item noti-title">
					<h5 class="m-0">
						<span class="float-right">
							<a href="javascript: void(0);" class="text-dark">
								<small>Limpar Tudo</small>
							</a>
						</span>
						Notificações
					</h5>
				</div>

				<div class="slimscroll">
					<notify-item v-for="notif in userNotif" :key="notif.id" :notif="notif"/>
				</div>

				<!-- All-->
				<a href="javascript:void(0);" v-if="userNotif.length>7" class="dropdown-item text-center text-primary notify-item notify-all">
					Ver tudo
				</a>

			</div>
		</li>

		<li class="dropdown notification-list">
			<a class="nav-link dropdown-toggle nav-user arrow-none mr-0" data-toggle="dropdown" href role="button" aria-haspopup="false"
				aria-expanded="false">
				<span class="account-user-avatar"> 
					<img :src="trelloUser.avatarUrl + '/50.png'" alt="user-image" class="rounded-circle">
				</span>
				<span>
					<span class="account-user-name">{{trelloUser.fullName}}</span>
					<span class="account-position text-info">@{{trelloUser.username}}</span>
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
import NotifyItem from '@/components/elements/NotifyItem'

export default {
	name: 'HeaderVue',
	components: {
		NotifyItem
	},
	data() {
		return {
			trelloUser: {},
			userNotif: [],
			hadNotif: false
		}
	},
	methods: {
		// Função inicializadora
		loadTrelloInfo() {
			this.getUserInfo()
			this.trelloNotifications()
		},
		// Função para fazer a busca das informações do usuário
		getUserInfo() {
			var vm = this
			// this.trelloStats = Trello.authorized()
			// if(!this.trelloStats) {
			// 	this.trelloLogin()
			// }
			Trello.members.get("me", function (member) {
				vm.trelloUser = member								
			})
		},
		// Função para login no trello
		trelloLogin() {				
			Trello.authorize({
				//type: 'popup',
				name: 'New Trello',
				scope: {
					read: 'true',
					write: 'true'
				},
				expiration: 'never',
				interactive: true,
				success: this.autoUpdate()
			})
		},
		// Função de logout do Trello
		trelloLogout() {
			clearInterval(this.updateDataInterval)

			Trello.deauthorize()
			this.trelloStats = Trello.authorized()
		},
		trelloNotifications() {
			var vm = this
			Trello.get(`members/${vm.trelloUser.id}/notifications`, notifications => {
				var unreads = []
				for(var notf of notifications) {
					if(notf.unread) {
						unreads.push(notf)
					}
				}
				if(vm.userNotif < unreads) {
					vm.hadNotif = true
				} else if(vm.userNotif[vm.userNotif.length-1].id != unreads[unreads.length-1].id) {
					vm.hadNotif = true
				}
				vm.userNotif = unreads
			})
		},
		// Função para atualizar a cada 1 segundos
		autoUpdate() {			
			this.updateDataInterval = setInterval(function () {
				this.loadTrelloInfo()
			}.bind(this), 1000)
		}
	},
	created() {
		this.trelloStats = Trello.authorized()
		if(!this.trelloStats) {
			this.trelloLogin()
		}
		this.loadTrelloInfo()

		$('.slimscroll').slimscroll({
			height: '300px',
			position: 'right',
            size: '8px',
            touchScrollStep: 20,
            color: '#9ea5ab'
		})
	},
	mounted() {
		$('.slimscroll').slimscroll({
			height: '300px',
			position: 'right',
            size: '8px',
            touchScrollStep: 20,
            color: '#9ea5ab'
		})
	}
}
</script>
