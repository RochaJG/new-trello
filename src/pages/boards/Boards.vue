<template>
    <span>
        <page-title title="Quadros">
            <bread-crumb-item goto="/" text="Home" ativo/>
            <bread-crumb-item text="Quadros"/>
        </page-title>
        
        <div class="row mb-2">
            <div class="col-sm-12">
                <div class="card">
                    <div class="card-body">
                        <h4 class="header-title">Escolha um quadro</h4>
                        <select class="custom-select mt-3" v-model="myBoard">
                            <option selected disabled>Escolha o quadro</option>
                            <option v-for="quadro in trelloBoards" :value="quadro" :key="quadro.id">{{quadro.name}}</option>
                        </select>
                    </div>
                </div>
            </div><!-- end col-->
        </div>

        <div class="row">
            <div class="col-md-6 col-xl-3" v-for="card in myBoard.cards" :key="card.id">
                <card-boards v-bind:card="card"/>
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
            trelloBoards: [],
            myBoard: {}
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