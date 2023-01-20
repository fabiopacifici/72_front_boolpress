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
      <template v-if="posts && !loading">
        <div class="row row-cols-1 row-cols-sm-3 g-4">
          <div class="col" v-for="post in posts.data">
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
      <template v-else-if="loading">
        <div class="loading">
          Loading ...
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
            class="bi bi-hourglass-split" viewBox="0 0 16 16">
            <path
              d="M2.5 15a.5.5 0 1 1 0-1h1v-1a4.5 4.5 0 0 1 2.557-4.06c.29-.139.443-.377.443-.59v-.7c0-.213-.154-.451-.443-.59A4.5 4.5 0 0 1 3.5 3V2h-1a.5.5 0 0 1 0-1h11a.5.5 0 0 1 0 1h-1v1a4.5 4.5 0 0 1-2.557 4.06c-.29.139-.443.377-.443.59v.7c0 .213.154.451.443.59A4.5 4.5 0 0 1 12.5 13v1h1a.5.5 0 0 1 0 1h-11zm2-13v1c0 .537.12 1.045.337 1.5h6.326c.216-.455.337-.963.337-1.5V2h-7zm3 6.35c0 .701-.478 1.236-1.011 1.492A3.5 3.5 0 0 0 4.5 13s.866-1.299 3-1.48V8.35zm1 0v3.17c2.134.181 3 1.48 3 1.48a3.5 3.5 0 0 0-1.989-3.158C8.978 9.586 8.5 9.052 8.5 8.351z" />
          </svg>
        </div>
      </template>
      <div v-else>
        <p> No posts here </p>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>

</style>