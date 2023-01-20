<script>
import axios from 'axios'
import AppBanner from '../components/AppBanner.vue'
export default {
  name: 'SinglePostView',
  components: { AppBanner },
  data() {
    return {
      post: null,
      loading: true,
      api_base_url: 'http://localhost:8001'
    }
  },
  mounted() {
    //console.log(this.$route.params.slug);
    const url = this.api_base_url + '/api/posts/' + this.$route.params.slug
    console.log(url);
    axios.get(url)
      .then(response => {
        if (response.data.success) {
          this.post = response.data.results
          this.loading = false
        } else {
          /* TODO: handle the not found post  
          404 
          */
          // https://router.vuejs.org/guide/essentials/navigation.html#navigate-to-a-different-location
        }
        console.log(response);
      }).catch(error => {
        console.log(error)
      })

  }
}
</script>

<template>
  <AppBanner :title="$route.params.slug" />
  <div class="single-post" v-if="post">
    <img class="img-fluid w-100" :src="api_base_url + '/storage/' + post.cover_image" :alt="post.title">
    <div class="container">
      <h2>
        {{ post.title }}
      </h2>
      <div class="content">
        {{ post.body }}
      </div>
    </div>
  </div>
</template>


<style lang="scss" scoped>

</style>