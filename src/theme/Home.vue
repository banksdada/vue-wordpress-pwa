<template>
  <div>
    <div class="columns category-posts" v-if="!posts || loading">
      <div class="column is-one-third" v-for="n in 6" v-bind:key="'skeleton-'+n">
        <div class="card fake-card">
          <div class="card-content">&nbsp;</div>
        </div>
      </div>
    </div>
    <div v-else>
      <div class="columns is-multiline category-posts">
        <div class="column is-one-third" v-for="post in posts" v-bind:key="post.id">
          <vwp-post-card :post="post"></vwp-post-card>
        </div>
      </div>
      <div class="home-empty" v-if="posts && posts.length === 0">
        <p>No posts yet. Start creating content in WordPress!</p>
      </div>
    </div>
  </div>
</template>

<script>
  import VwpPostCard from 'components/vwpPostCard.vue'
  import wordpressService from '../app.service'

  export default {
    name: 'HomePage',
    components: {
      'vwp-post-card': VwpPostCard
    },
    data () {
      return {
        posts: [],
        loading: true
      }
    },
    mounted () {
      this.loadPosts()
    },
    methods: {
      loadPosts () {
        this.loading = true
        wordpressService.getAllPosts(1, 12).then((data) => {
          this.posts = data.posts
          this.loading = false
        }).catch(() => {
          this.loading = false
        })
      }
    }
  }
</script>

<style lang="scss">
  @import '../_variables';

  .home-empty {
    text-align: center;
    padding: 3rem;
    color: $text-secondary;
  }
</style>
