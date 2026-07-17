<template>
  <div>
    <div class="card personal-card" v-if="categories && categories.length === 1 && categories[0].slug === 'uncategorized'">
      <div class="welcome-content">
        <div class="welcome-icon">
          <span class="welcome-emoji">&#128640;</span>
        </div>
        <div class="welcome-text">
          <h2>Welcome to BaseUse</h2>
          <p>Your digital workspace powered by WordPress &amp; Vue.js PWA. Explore the latest posts below.</p>
        </div>
      </div>
    </div>
    <div class="clearfix"></div>
    <div class="columns category-posts" v-if="!categories || categories.length === 0">
      <div class="column is-one-third" v-for="n in 6" v-bind:key="'skeleton-'+n">
        <div class="card fake-card">
          <div class="card-content">&nbsp;</div>
        </div>
      </div>
    </div>
    <vwp-subcategory :categories="categories"></vwp-subcategory>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import VwpSubcategory from 'components/vwpSubcategory.vue'
const fetchInitialData = (store, route) => {
  route.params.page = route.params.page || 1
  return store.dispatch('category/getCategory', {categorySlug: route.params.id, page: route.params.page})
}
export default {
  name: 'ThemePageCategory',
  components: {
    'vwp-subcategory': VwpSubcategory
  },
  computed: {
    ...mapGetters('category', ['categories'])
  },
  methods: {
    loadPosts () {
      fetchInitialData(this.$store, this.$route)
    }
  },
  watch: {
    '$route' (to, from) {
      this.loadPosts()
    }
  },
  prefetch: fetchInitialData,
  mounted () {
    this.loadPosts()
  }
}
</script>

<style lang="scss">
  @import '../variables';

  .personal-card {
    background: linear-gradient(135deg, rgba($primary, 0.05), rgba($accent, 0.05));
    border: 1px solid rgba($primary, 0.1);
    border-radius: $radius;
    padding: 2rem !important;
    margin-bottom: 2rem;
    transition: transform $transition-smooth, box-shadow $transition-smooth;
    &:hover {
      transform: translateY(-2px);
      box-shadow: $card-hover-shadow;
    }
  }

  .welcome-content {
    display: flex;
    align-items: center;
    gap: 1.5rem;
  }

  .welcome-icon {
    flex-shrink: 0;
  }

  .welcome-emoji {
    font-size: 3rem;
  }

  .welcome-text {
    h2 {
      font-size: 1.5rem;
      font-weight: 700;
      margin-bottom: 0.5rem;
    }
    p {
      color: $text-secondary;
      margin: 0;
      line-height: 1.5;
    }
  }
</style>
