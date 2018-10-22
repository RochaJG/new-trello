<template>
    <a :href="'https://trello.com/c/' + notif.data.card.shortLink" target="_blank" class="dropdown-item notify-item">
        <div :class="'notify-icon bg-' + infoToNotif.color">
            <i :class="'mdi mdi-'+ infoToNotif.icon"></i>
        </div>
        <p class="notify-details" v-if="notif.memberCreator">{{notif.memberCreator.fullName}}</p>
        <p class="text-muted mb-0 user-msg">
            <b>{{infoToNotif.message}}{{notif.data.card.name}}</b>
            <br>
            <small>há {{notif.elapsedTime}}</small>
        </p>
    </a>
</template>

<script>
export default {
    name: 'NotifyItem',
    props: {
        notif: Object
    },
    data() {
        return {
            dictonary: [
                {
                    type: 'addAttachmentToCard',
                    message: 'Anexou um arquivo ao cartão: ',
                    color: 'info',
                    icon: 'attachment'
                }
            ]
        }
    },
    methods: {
        calcElapsedTime() {
            let vm = this
            let diff = moment().diff(moment(vm.notif.date), 'minutes')

            if(diff < 60) {
                vm.$set(vm.notif, 'elapsedTime', `${diff} minutos`)
            } else {
                diff = moment().diff(moment(vm.notif.date), 'hours')
                if(diff < 60) {
                    vm.$set(vm.notif, 'elapsedTime', `${diff} horas`)
                } else {
                    diff = moment().diff(moment(vm.notif.date), 'days')
                    vm.$set(vm.notif, 'elapsedTime', `${diff} dias`)
                }
            }
        }
    },
    computed: {
        infoToNotif() {
            var resp = {
                        color: 'primary',
                        icon: 'alert-circle',
                        message: 'Atividade no cartão: '
                    }
            for(var dict of this.dictonary) {
                if(this.notif.type == dict.type) {
                    resp = dict
                }
            }

            return resp
        }
    },
    created() {
        this.calcElapsedTime()
    },
    updated() {
        this.calcElapsedTime()
    }
}
</script>
