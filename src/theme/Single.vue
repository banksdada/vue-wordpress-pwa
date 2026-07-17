<template>
  <div>
    <div v-if="single && !single.content">
      <div class="loading-state">
        <div class="loading-spinner"></div>
        <p>Loading...</p>
      </div>
      <div class="single-content card fake-single-content"></div>
    </div>
    <vwp-single :single="single"></vwp-single>
  </div>
</template>

<script>
  import { mapGetters, mapActions } from 'vuex'
  import VwpSingle from 'components/vwpSingle.vue'
  const fetchInitialData = (store, route) => {
    return store.dispatch('category/getPost', route.params.id)
  }
  export default {
    name: 'SingleComponent',
    components: {
      'vwp-single': VwpSingle
    },
    computed: {
      ...mapGetters(['routeParamId']),
      ...mapGetters('category', ['single'])
    },
    methods: {
      ...mapActions('category', {
        getPost: 'getPost'
      }),
      loadData () {
        fetchInitialData(this.$store, this.$route)
      }
    },
    watch: {
      $route (to, from) {
        this.loadData()
      }
    },
    prefetch: fetchInitialData,
    mounted () {
      this.loadData()
    }
  }
</script>

<style lang="scss">
  @import '../_variables';

  .loading-state {
    text-align: center;
    padding: 3rem;
    color: $text-secondary;
  }

  .loading-spinner {
    width: 40px;
    height: 40px;
    border: 3px solid $border-color;
    border-top-color: $primary;
    border-radius: 50%;
    margin: 0 auto 1rem;
    animation: spin 0.8s linear infinite;
  }

  @keyframes spin {
    to { transform: rotate(360deg); }
  }
</style>
