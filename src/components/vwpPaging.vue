<template>
  <div class="vwp-paging">
    <div class="paging-wrapper">
      <template v-for="(item) in pages">
        <router-link
          v-if="item !== '...'"
          v-bind:key="item"
          v-bind:class="{ 'is-active': ((page == null && item === 1) || (item === page)) }"
          :to="path + '/page/' + item + '/'"
          class="page-link"
        >{{ item }}</router-link>
        <span v-else v-bind:key="'dots-'+item" class="page-dots">...</span>
      </template>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['totalPages', 'path'],
    data () {
      return {
        pages: [],
        neighboors: 2,
        page: 1
      }
    },
    watch: {
      $route (to, from) {
        this.page = to.params.page
        this.refreshPages(this.page)
      }
    },
    methods: {
      refreshPages: function (page) {
        if (!page) page = 1
        page = parseInt(page)
        this.pages = []
        for (var i = 1; i <= this.totalPages; i++) {
          if (i === 1 || i === parseInt(this.totalPages)) {
            this.pages.push(i)
          } else if ((i >= page - this.neighboors && i <= page) || (i >= page && i <= page + this.neighboors)) {
            this.pages.push(i)
          } else if (i === page - this.neighboors - 1 || i === page + this.neighboors + 1) {
            this.pages.push('...')
          }
        }
      }
    },
    created () {
      this.page = 1
      if (this.$route.params && this.$route.params.page) {
        this.page = this.$route.params.page
      }
      this.refreshPages(this.page)
    }
  }
</script>

<style lang="scss">
  @import '../_variables';

  .vwp-paging {
    padding: 2rem 0;
    text-align: center;
  }

  .paging-wrapper {
    display: inline-flex;
    gap: 0.5rem;
    align-items: center;
  }

  .page-link {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-width: 40px;
    height: 40px;
    padding: 0 12px;
    border-radius: 10px;
    font-weight: 600;
    font-size: 0.9rem;
    color: $primary;
    background: transparent;
    border: 1px solid rgba($primary, 0.2);
    transition: all $transition-fast;
    text-decoration: none;

    &:hover {
      background: rgba($primary, 0.08);
      border-color: $primary;
    }

    &.is-active {
      background: linear-gradient(135deg, $gradient-start, $gradient-end);
      color: white;
      border-color: transparent;
      box-shadow: 0 4px 12px rgba($primary, 0.3);
    }
  }

  .page-dots {
    color: $text-secondary;
    padding: 0 4px;
  }
</style>
