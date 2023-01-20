<script>
import AppBanner from '../components/AppBanner.vue';
import PostsList from '../components/PostsList.vue';
export default {
  name: 'BlogView',
  components: { AppBanner, PostsList },
  data() {
    return {
      pageTitle: 'Blog'
    }
  }

}
</script>

<template>
  <AppBanner :title="pageTitle" />
  <PostsList />

</template>


<style lang="scss" scoped>

</style>