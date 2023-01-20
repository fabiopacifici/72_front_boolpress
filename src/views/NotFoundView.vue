<script>
import AppBanner from '../components/AppBanner.vue';
export default {
  name: 'NotFoundView',
  components: { AppBanner }

}
</script>

<template>
  <AppBanner title="404" />
  <div class="container">
    <p class="lead">
      😨 Ops, Page not found!
    </p>
    <router-link to="/">Go to Homepage</router-link>

  </div>

</template>


<style lang="scss" scoped>

</style>