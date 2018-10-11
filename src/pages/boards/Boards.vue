<template>
    <span>
        <page-title title="Quadros">
            <bread-crumb-item goto="/" text="Home" ativo/>
            <bread-crumb-item text="Quadros"/>
        </page-title>
        
        <div class="row mb-2">
            <div class="col-sm-12">
                <div class="text-sm-right">
                    <div class="btn-group mb-3">
                        <button type="button" class="btn btn-primary">Todos</button>
                    </div>
                    <div class="btn-group mb-3 ml-1">
                        <button type="button" class="btn btn-light">Atuais</button>
                        <button type="button" class="btn btn-light">Finalizados</button>
                    </div>
                    <div class="btn-group mb-3 ml-2 d-none d-sm-inline-block">
                        <button type="button" class="btn btn-dark"><i class="dripicons-view-apps"></i></button>
                    </div>
                    <div class="btn-group mb-3 d-none d-sm-inline-block">
                        <button type="button" class="btn btn-link text-dark"><i class="dripicons-checklist"></i></button>
                    </div>
                </div>
            </div><!-- end col-->
        </div>

        <div class="row">
            <div class="col-md-6 col-xl-3">
                <card-boards/>
            </div>
        </div>
    </span>
</template>

<script>
import PageTitle from '@/components/layouts/PageTitle'
import BreadCrumbItem from '@/components/layouts/BreadCrumbItem'
import CardBoards from '@/components/elements/CardBoards'

export default {
    name: 'Boards',
    components: {
        PageTitle,
        BreadCrumbItem,
        CardBoards,
    },
    data() {
        return {
        }
    },
    methods: {
        getData() {
            var vm = this
            this.updateLoggedIn()

            Trello.members.get("me", function (member) {
                vm.trelloUser = member

                // Busca as boards do usuário
                Trello.get("members/me/boards", function (boards) {
                    $.each(boards, function (ix, board) {
                        //Busca cards abertas de cada board do usuário
                        Trello.get(`boards/${board.shortLink}/cards/open`, function (cards) {
                            var myCards = []
                            $.each(cards, function (ix, card) {
                                $.each(card.idMembers, function (ix, member) {
                                    if (member == vm.trelloUser.id) {
                                        myCards.push(card)
                                    }
                                })
                            })
                            board.cards = myCards
                        })
                    })
                    vm.trelloBoards = boards
                    console.log(vm.trelloBoards)
                    console.log("------FIM-----")
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
    mounted() {
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