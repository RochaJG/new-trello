<template>
    <div class="row">
        <div class="col-12">
            <div class="page-title-box">
                <div class="page-title-right">
                    <ol class="breadcrumb m-0">
                        <slot></slot>
                    </ol>
                </div>
                <h4 class="page-title">{{title}}</h4>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'PageTitle',
    props: ['title']
}
</script>
