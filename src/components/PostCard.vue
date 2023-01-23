<script>
import { state } from '../state.js'
export default {
  name: 'PostCard',
  props: {
    post: Object
  },
  data() {
    return {
      state,
      max: 100
    }
  },
  methods: {
    getImagePath(path) {
      console.log(path);
      if (path) {
        return this.state.api_base_url + '/storage/' + path
      }
      return '/img/placeholder_600.png'
    },
    /**
     * 
     * @param {string} text the post body
     */
    trimBody(text) {
      console.log(text);
      if (text.length > this.max) {
        return text.slice(0, this.max) + '...'
      }
      return text
    },
  }
}
</script>
<template>
  <div class="col">
    <div class="card border-0 shadow-sm rounded-0 rounded-bottom">
      <img class="card-image rounded-top" :src="getImagePath(post.cover_image)" alt="">
      <div class="card-body">
        <h4>{{ post.title }}</h4>
        <p>
          {{ trimBody(post.body) }}
        </p>
        <router-link :to="{ name: 'single-post', params: { slug: post.slug } }">Read more</router-link>
      </div>
      <div class="card-footer text-muted">
        <div class="category">
          <strong>Category: </strong>
          <span v-if="post.category">
            {{ post.category.name }}
          </span>
          <span v-else>Uncategorized</span>
        </div>
        <div class="tags">
          <strong>Tags: </strong>
          <template v-if="post.tags.lenght > 0">
            <span v-for="tag in post.tags">
              #{{ tag.name }}
            </span>
          </template>
          <template v-else>
            <span>No tags.</span>
          </template>
        </div>
      </div>

    </div>
  </div>
</template>

<style lang="scss" scoped>

</style>