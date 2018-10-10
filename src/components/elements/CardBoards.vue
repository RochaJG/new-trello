<template>
    <div class="card d-block">
        <div class="card-body">
            <div class="dropdown card-widgets">
                <a href class="dropdown-toggle arrow-none" data-toggle="dropdown" aria-expanded="false">
                    <i class="dripicons-dots-3"></i>
                </a>
                <div class="dropdown-menu dropdown-menu-right">
                    <!-- item-->
                    <a href class="dropdown-item"><i class="mdi mdi-pencil mr-1"></i>Edit</a>
                    <!-- item-->
                    <a href class="dropdown-item"><i class="mdi mdi-delete mr-1"></i>Delete</a>
                    <!-- item-->
                    <a href class="dropdown-item"><i class="mdi mdi-email-outline mr-1"></i>Invite</a>
                    <!-- item-->
                    <a href class="dropdown-item"><i class="mdi mdi-exit-to-app mr-1"></i>Leave</a>
                </div>
            </div>
            <!-- project title-->
            <h4 class="mt-0">
                <a href class="text-dark">App design and development</a>
            </h4>
            <div class="badge badge-success badge-pill">Finished</div>

            <p class="text-muted font-13 mb-3">With supporting text below as a natural lead-in to additional contenposuere erat a ante...<a href class="font-weight-bold text-muted">view more</a>
            </p>

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
                <a href data-toggle="tooltip" data-placement="top" title="" data-original-title="Mat Helme" class="d-inline-block">
                    <img src="/static/img/profile.png" class="rounded-circle avatar-xs" alt="friend">
                </a>

                <a href class="d-inline-block text-dark font-weight-bold ml-2">
                    +7 more
                </a>
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
    props: {}
}
</script>
