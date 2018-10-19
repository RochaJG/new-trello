<template>
    <span>
        <page-title title="Quadros">
            <bread-crumb-item goto="/" text="Home" ativo/>
            <bread-crumb-item text="Quadros"/>
        </page-title>
        
        <div class="row" v-for="org in trelloOrgs" :key="org.id">
            <h3 class="col-12">{{org.displayName}}</h3>
            <h6 class="col-12">{{org.desc}}</h6>
            <div class="col-3" v-for="board in org.boards" :key="board.id">
                <board-item :board="board" />
            </div><!-- end col-->
        </div>
    </span>
</template>

<script>
import PageTitle from '@/components/layouts/PageTitle'
import BreadCrumbItem from '@/components/layouts/BreadCrumbItem'
import BoardItem from '@/components/elements/BoardItem'

export default {
    name: 'Boards',
    components: {
        PageTitle,
        BreadCrumbItem,
        BoardItem,
    },
    data() {
        return {
            trelloOrgs: []
        }
    },
    methods: {
        getData() {
            var vm = this
            this.updateLoggedIn()

            Trello.members.get("me", function (member) {
                vm.trelloUser = member

                // Busca organizações do usuário
                Trello.get(`members/me/organizations`, function(orgs) {
                    vm.trelloOrgs = orgs

                    $.each(orgs, function (ix, org) {
                        // Busca as boards do usuário de acordo com a organização
                        Trello.get(`organizations/${org.id}/boards`, function (boards) {
                            vm.$set(org, 'boards', boards)
                        })
                    })
                })
            })
        },
        updateLoggedIn () {
            this.trelloStats = Trello.authorized()
        },
        trelloLogout () {
            Trello.deauthorize()
            this.updateLoggedIn()
        },
        trelloLogin () {
            Trello.authorize({
                type: "popup",
                success: this.getData
            })
        }
    },
    created() {
        this.trelloStats = Trello.authorized()
        if(!this.trelloStats) {
            Trello.authorize({
                type: 'popup',
                name: 'New Trello',
                interactive: true,
                success: this.getData,
            })
        } else {
            this.getData()
        }
    },
}
</script>