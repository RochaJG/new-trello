<template>
    <div class="card d-block">
        <div class="card-body">
            <div class="dropdown card-widgets">
                <a href class="dropdown-toggle arrow-none" data-toggle="dropdown" aria-expanded="false">
                    <i class="dripicons-dots-3"></i>
                </a>
                <div class="dropdown-menu dropdown-menu-right">
                    <!-- item-->
                    <a href class="dropdown-item"><i class="mdi mdi-pencil mr-1"></i>Editar</a>
                </div>
            </div>
            <!-- project title-->
            <h4 class="mt-0">
                <a :href="card.shortUrl" target="_blank" class="text-dark">{{card.name}}</a>
            </h4>
            <div v-for="badge in card.labels" :key="badge.id" :class="'badge badge-' + badge.color + ' badge-pill'">{{badge.name}}</div>

            <p class="text-muted font-13 mb-3" v-html="card.desc.URLToAnchors()"></p>

            <!-- project detail-->
            <p class="mb-1">
                <span class="pr-2 text-nowrap mb-2 d-inline-block">
                    <i class="mdi mdi-format-list-bulleted-type text-muted"></i>
                    <b>21</b> Tasks
                </span>
                <span class="text-nowrap mb-2 d-inline-block">
                    <i class="mdi mdi-comment-multiple-outline text-muted"></i>
                    <b>741</b> Comments
                </span>
            </p>
            <div>
                <!-- <a href data-toggle="tooltip" data-placement="top" title="" :data-original-title="card.members[0].fullName" class="d-inline-block">
                    <img :src="card.members[0].avatarUrl + '/50.png'" class="rounded-circle avatar-xs" alt="Membro" v-if="card.members[0].avatarUrl">
                </a> -->

                <a class="d-inline-block text-dark font-weight-bold ml-2" v-if="card.idMembers.length">{{card.idMembers.length}} membros</a>
            </div>
        </div> <!-- end card-body-->
        <ul class="list-group list-group-flush">
            <li class="list-group-item p-3">
                <!-- project progress-->
                <p class="mb-2 font-weight-bold">Progresso <span class="float-right">100%</span></p>
                <div class="progress progress-sm">
                    <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%;">
                    </div><!-- /.progress-bar -->
                </div><!-- /.progress -->
            </li>
        </ul>
    </div> <!-- end card-->
</template>

<script>
export default {
    name: 'CardBoards',
    props: {
        card: Object
    },
    mounted() {
        var card = this.card
        card.members = []
        $.each(card.idMembers, (ix, id) => {
            Trello.get(`members/${id}`, (member) => {
                card.members.push(member)
            })
        })
    }
}
</script>

<style scoped>
.badge-red {
    color: #fff;
    background-color: #f9375e;
    border-color: #f82b54;
}

.badge-orange {
    color: #fff;
    background-color: #FF5722;
    border-color: rgb(255, 78, 24);
}

.badge-black {
    color: #fff;
    background-color: #37474F;
    border-color: #263238;
}

.badge-green {
    color: #fff;
    background-color: #7CB342;
    border-color: #689F38;
}
</style>
