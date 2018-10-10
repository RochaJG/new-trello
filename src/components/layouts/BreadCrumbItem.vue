<template>
    <li :class="'breadcrumb-item ' + (ativo ? 'active' : '')">
        <span v-if="!ativo">{{text}}</span>
        <router-link v-if="ativo" :to="goto">{{text}}</router-link>
    </li>
</template>

<script>
export default {
    name: 'BreadCrumbItem',
    props: {
        ativo: Boolean, 
        goto: String, 
        text: String
    }
}
</script>
