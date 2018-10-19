<template>
    <div class="card text-white" :style="'background-color: ' + (board.prefs.backgroundColor ? board.prefs.backgroundColor : '#0079BF') + ' !important;'">
        <div class="card-body">
            <h5 class="card-title"><a class="text-white" :href="board.shortUrl" target="_blank">{{board.name}}</a></h5>
            <p class="card-text">{{board.desc}}</p>
            <span class="span-info" data-toggle="tooltip" data-placement="top" :data-original-title="board.memberships.length + ' membros'">
                <i class="mdi mdi-account-multiple"></i> {{board.memberships.length}}
            </span>
            <span class="span-info" data-toggle="tooltip" data-placement="top" :data-original-title="board.cards.length + ' cards'">
                <i class="mdi mdi-library-books"></i> {{board.cards.length}}
            </span>
            <br>
            <span class="span-info" data-toggle="tooltip" data-placement="top" :data-original-title="'Última' + board.ultmovMsg">
                <i :class="'mdi mdi-'+ board.iconmov"></i> {{board.ultmov}}
            </span>
        </div> <!-- end card-body-->
    </div> <!-- end card-->
</template>

<script>
export default {
    name: 'BoardItem',
    props: ['board'],
    methods: {
        updateInfo() {
            this.getBoardInfo()
            $('[data-toggle="tooltip"]').tooltip()
        },
        getBoardInfo() {
            let vm = this
            //Busca cards abertas de cada board do usuário
            Trello.get(`boards/${vm.board.shortLink}/cards/open`, function (cards) {
                vm.$set(vm.board, 'cards', cards)
            })
        },
        // Função para atualizar a cada 1,5 segundos
		autoUpdate() {			
			this.updateDataInterval = setInterval(function () {
				this.updateInfo()
			}.bind(this), 1500)
		}
    },
    created() {
        let vm = this
        vm.$set(vm.board, 'cards', [])
        //Busca cards abertas de cada board do usuário
        Trello.get(`boards/${vm.board.shortLink}/cards/open`, function (cards) {
            vm.$set(vm.board, 'cards', cards)
        })

        $('[data-toggle="tooltip"]').tooltip()

        if(this.board.dateLastActivity) {
            this.$set(this.board, 'ultmov', moment(this.board.dateLastActivity).format('DD/MM/YYYY HH:mm'))
            this.$set(this.board, 'ultmovMsg', ' movimentação')
            this.$set(this.board, 'iconmov', 'clock')
        } else {
            this.$set(this.board, 'ultmov', moment(this.board.dateLastView).format('DD/MM/YYYY HH:mm'))
            this.$set(this.board, 'ultmovMsg', ' visualização')
            this.$set(this.board, 'iconmov', 'eye')
        }
    },
    mounted() {
        this.autoUpdate()
    }
}
</script>

<style scoped>
    span.span-info {
        cursor: default;
    }
</style>
