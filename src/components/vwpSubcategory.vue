<template>
  <div class="vwp-subcategory">
    <div v-for="category in categories" v-bind:key="category.id">
      <div class="category-header" v-if="categories.length > 1">
        <h2>
          <router-link :to="'/category/' + category.slug + '/'">
            <span>{{ category.name }}</span>
          </router-link>
        </h2>
      </div>
      <div class="columns category-posts" v-if="!category.posts || category.posts.length === 0">
        <div class="column is-one-third" v-for="n in 6" v-bind:key="'skeleton-'+n">
          <div class="card fake-card">
            <div class="card-content">&nbsp;</div>
          </div>
        </div>
      </div>
      <div class="columns is-multiline category-posts category-posts-loaded">
        <div class="column is-one-third" v-for="(item) in category.posts" v-bind:key="item.id">
          <vwp-post-card :post="item" :newFlag="newFlag" :categorySlug="category.slug"></vwp-post-card>
        </div>
      </div>
      <div v-if="!hidePagination">
        <vwp-paging v-if="category.totalPages > 0" :totalPages="category.totalPages" :path="'/category/' + category.slug"></vwp-paging>
      </div>
    </div>
  </div>
</template>

<script>
  import VwpPostCard from './vwpPostCard.vue'
  import VwpPaging from './vwpPaging.vue'
  export default {
    name: 'vwp-subcategory',
    components: {
      'vwp-post-card': VwpPostCard,
      'vwp-paging': VwpPaging
    },
    props: ['hidePagination', 'newFlag', 'categories']
  }
</script>

<style lang="scss">
  @import '../variables';

  .vwp-subcategory {
    .category-header {
      margin-bottom: 1.5rem;
      h2 {
        font-size: 1.5rem;
        font-weight: 700;
        a { color: $text-primary !important; }
      }
    }

    .category-posts {
      animation: fadeIn 0.5s ease-out;
    }

    .category-posts-loaded .column {
      animation: fadeInUp 0.4s ease-out both;
      &:nth-child(1) { animation-delay: 0s; }
      &:nth-child(2) { animation-delay: 0.05s; }
      &:nth-child(3) { animation-delay: 0.1s; }
      &:nth-child(4) { animation-delay: 0.15s; }
      &:nth-child(5) { animation-delay: 0.2s; }
      &:nth-child(6) { animation-delay: 0.25s; }
    }
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  @keyframes fadeInUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
</style>
