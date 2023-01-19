<script>
import axios from 'axios';

export default {
  name: 'AppMain',
  data() {
    return {
      posts: null,
      base_api_url: 'http://localhost:8001',
      loading: true,
      error: null,
      max: 100

    }
  },
  methods: {
    getPosts(url) {
      // ajax call to get all posts
      axios
        .get(url)
        .then(response => {
          console.log(response.data.results);
          this.posts = response.data.results;
          this.loading = false
        })
        .catch(error => {
          console.error(error)
          this.error = error.message
          this.loading = false
        })
    },
    getImagePath(path) {
      console.log(path);
      if (path) {
        return this.base_api_url + '/storage/' + path
      }
      return '/img/placeholder_600.png'
    },
    /**
     * 
     * @param {string} text the post body
     */
    trimBody(text) {
      if (text.length > this.max) {
        return text.slice(0, this.max) + '...'
      }
      return text
    },
    prevPage(url) {
      console.log(url)
      this.getPosts(url)
    },
    nextPage(url) {
      console.log(url)
      this.getPosts(url)
    }

  },
  mounted() {
    this.getPosts(this.base_api_url + '/api/posts');
  }

}
</script>

<template>

  <section class="vue-home pt-5">
    <div class="container">
      <template v-if="posts">
        <div class="row row-cols-1 row-cols-sm-3 g-4">
          <div class="col" v-for="post in posts.data">
            <div class="card border-0 shadow-sm rounded-0 rounded-bottom">
              <img class="card-image rounded-top" :src="getImagePath(post.cover_image)" alt="">
              <div class="card-body">
                <h4>{{ post.title }}</h4>
                <p>
                  {{ trimBody(post.body) }}
                </p>
                <a href="#">Read more</a>
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
        </div>

        <nav aria-label="Page navigation" class="d-flex justify-content-center pt-5">
          <ul class="pagination    ">
            <li class="page-item" v-if="posts.prev_page_url" @click="prevPage(posts.prev_page_url)">
              <a class="page-link" aria-label="Previous">
                <span aria-hidden="true">&laquo;</span>
              </a>
            </li>
            <li class="page-item active" aria-current="page"><a class="page-link" href="#">{{
              posts.current_page
            }}</a></li>

            <li class="page-item" v-if="posts.next_page_url" @click="nextPage(posts.next_page_url)">
              <a class="page-link" aria-label="Next">
                <span aria-hidden="true">&raquo;</span>
              </a>
            </li>
          </ul>
        </nav>

      </template>
      <div v-else>
        <p> No posts here </p>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>

</style>