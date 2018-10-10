<template>
    <li class="side-nav-item">
        <router-link class="side-nav-link" :to="goto">
            <i :class="'mdi mdi-' + icon"></i>
            <span> {{title}} </span>
        </router-link>
    </li>
</template>

<script>
export default {
    name: 'MenuLink',
    props: ['goto', 'title', 'icon']
}
</script>
