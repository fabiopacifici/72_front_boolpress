<script>
import AppNav from './components/AppNav.vue'
import AppBanner from './components/AppBanner.vue'
import AppMain from './components/AppMain.vue'

export default {
    components: {
        AppNav,
        AppBanner,
        AppMain

    },


}
</script>

<template>

    <AppNav></AppNav>
    <AppBanner></AppBanner>
    <AppMain></AppMain>

</template>

<style lang="scss">
@use './styles/general.scss';
</style>
