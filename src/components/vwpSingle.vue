<template>
  <div class="vwp-single">
    <div v-if="single && single.content">
      <div v-show="!hideBack" class="single-nav">
        <router-link :to="'/category/' + single.pure_taxonomies.categories[0].slug + '/'" class="back-button">
          <span class="arrow-left">&larr;</span>
          <span>{{ single.pure_taxonomies.categories[0].name }}</span>
        </router-link>
      </div>
      <div class="single-header">
        <h1 v-html="single.title.rendered"></h1>
        <div class="single-meta">
          <span class="single-date">{{ formatDate(single.date) }}</span>
          <div class="single-tags" v-if="single.tags && single.tags.length > 0">
            <span class="tag" v-for="tag in single.pure_taxonomies.tags" v-bind:key="tag.id">{{ tag.name }}</span>
          </div>
        </div>
      </div>
      <div class="single-content card">
        <div class="card-content">
          <div v-html="single.content.rendered"></div>
          <div v-if="single.rest_api_enabler && single.rest_api_enabler.Link" class="single-link">
            <a :href="single.rest_api_enabler.Link" target="_blank">{{ single.rest_api_enabler.Link }}</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['single', 'hideBack'],
    methods: {
      formatDate: function (dateStr) {
        return new Date(dateStr).toLocaleDateString('en-US', { month: 'long', day: 'numeric', year: 'numeric' })
      }
    }
  }
</script>

<style lang="scss">
  @import '../variables';

  .vwp-single {
    max-width: 800px;
    margin: 0 auto;

    pre {
      white-space: pre-wrap;
      word-wrap: break-word;
      background: rgba(0,0,0,0.03);
      padding: 1rem;
      border-radius: $radius-sm;
    }

    .single-nav {
      margin-bottom: 1.5rem;
    }

    .back-button {
      display: inline-flex;
      align-items: center;
      gap: 0.5rem;
      font-weight: 600;
      color: $primary !important;
      transition: all $transition-fast;
      .arrow-left { transition: transform $transition-fast; display: inline-block; }
      &:hover .arrow-left { transform: translateX(-4px); }
    }

    .single-header {
      margin-bottom: 2rem;
      h1 {
        font-size: 2.25rem;
        font-weight: 800;
        line-height: 1.2;
        margin-bottom: 0.75rem;
      }
    }

    .single-meta {
      display: flex;
      align-items: center;
      gap: 1rem;
      flex-wrap: wrap;
    }

    .single-date {
      color: $text-secondary;
      font-size: 0.9rem;
    }

    .single-tags {
      display: flex;
      gap: 0.5rem;
      .tag {
        background: linear-gradient(135deg, rgba($primary, 0.1), rgba($accent, 0.1));
        color: $primary;
        font-size: 0.75rem;
        font-weight: 600;
        padding: 2px 10px;
        border-radius: 20px;
        border: none;
      }
    }

    .single-content {
      border-radius: $radius;
      box-shadow: $card-shadow;
      .card-content {
        font-size: 1.05rem;
        line-height: 1.8;
      }
    }

    .single-link {
      margin-top: 1.5rem;
      padding-top: 1rem;
      border-top: 1px solid $border-color;
      a { color: $primary !important; }
    }
  }
</style>
