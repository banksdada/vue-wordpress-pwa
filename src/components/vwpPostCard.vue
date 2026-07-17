<template>
  <div :class="{'vwp-post-card': true, 'card':true, 'new':isNew(post.date)}">
    <div class="card-image" v-if="post.better_featured_image && post.better_featured_image.media_details && post.better_featured_image.media_details.sizes.medium">
      <figure class="image">
        <clazy-load v-bind:src="cdnUrl(post.better_featured_image.media_details.sizes.medium.source_url)">
          <img v-bind:alt="post.title.rendered" v-bind:src="cdnUrl(post.better_featured_image.media_details.sizes.medium.source_url)" slot="image" />
          <div slot="placeholder" class="image-placeholder"></div>
        </clazy-load>
      </figure>
    </div>
    <div class="card-image placeholder-image" v-else>
      <div class="image-placeholder-gradient">
        <span class="placeholder-icon">&#9998;</span>
      </div>
    </div>
    <div class="card-content" v-if="post && post.title">
      <div class="content">
        <div v-if="isNew(post.date)" class="new-badge">NEW</div>
        <div class="post-meta">
          <small>{{ formatDate(post.date) }}</small>
        </div>
        <div class="post-title">
          <a v-on:click="gotoPost(post)">
            <span v-html="post.title.rendered"></span>
          </a>
        </div>
        <div class="post-excerpt" v-html="post.excerpt.rendered"></div>
      </div>
    </div>
    <footer class="card-footer">
      <router-link :to="'/category/' + categorySlug + '/' + post.slug" class="card-footer-item read-more">
        Read More <span class="arrow">&rarr;</span>
      </router-link>
    </footer>
  </div>
</template>

<script>
  import Config from '../app.config.js'
  export default {
    name: 'vwp-post-card',
    props: ['post', 'categorySlug', 'newFlag'],
    methods: {
      gotoPost: function (post) {
        if (this.categorySlug && post && post.slug) {
          this.$router.push({ path: '/category/' + this.categorySlug + '/' + post.slug })
        }
      },
      cdnUrl: function (url) {
        return url.replace('https://api.fullstackweekly.com/', Config.wpDomain)
      },
      isNew: function (postDateStr) {
        let postDate = new Date(postDateStr)
        postDate.setDate(postDate.getDate() + 6)
        return this.newFlag && postDate.getTime() - new Date().getTime() > 0
      },
      formatDate: function (dateStr) {
        return new Date(dateStr).toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' })
      }
    }
  }
</script>

<style lang="scss">
  @import '../variables';

  .vwp-post-card {
    min-height: 380px;
    height: 100%;
    border-radius: $radius;
    overflow: hidden;
    border: 1px solid $border-color;
    transition: transform $transition-smooth, box-shadow $transition-smooth;
    position: relative;
    background: $card-bg;

    &:hover {
      transform: translateY(-6px);
      box-shadow: $card-hover-shadow;
    }

    &.new {
      border-color: $accent;
      &::before {
        content: '';
        position: absolute;
        top: 0; left: 0; right: 0;
        height: 3px;
        background: linear-gradient(90deg, $accent, $primary);
        z-index: 2;
      }
    }

    .card-image {
      overflow: hidden;
      .image img {
        max-height: 200px;
        width: 100%;
        object-fit: cover;
        transition: transform 0.6s ease;
      }
    }

    &:hover .card-image .image img {
      transform: scale(1.05);
    }

    .placeholder-image {
      height: 160px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .image-placeholder-gradient {
      width: 100%;
      height: 100%;
      background: linear-gradient(135deg, $gradient-start, $gradient-end);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .placeholder-icon {
      font-size: 2.5rem;
      opacity: 0.4;
    }

    .image-placeholder {
      width: 100%;
      height: 200px;
      background: linear-gradient(135deg, #f0f0f0 25%, #e8e8e8 50%, #f0f0f0 75%);
      background-size: 200% 100%;
      animation: shimmer 1.5s ease-in-out infinite;
    }

    .card-content {
      padding: 1.25rem;
      .content { word-break: normal; word-wrap: break-word; }
    }

    .new-badge {
      display: inline-block;
      background: linear-gradient(135deg, $accent, $primary);
      color: white;
      font-size: 0.65rem;
      font-weight: 700;
      padding: 2px 8px;
      border-radius: 4px;
      letter-spacing: 1px;
      margin-bottom: 0.5rem;
    }

    .post-meta {
      color: $text-secondary;
      font-size: 0.8rem;
      margin-bottom: 0.5rem;
    }

    .post-title {
      margin-bottom: 0.75rem;
      a {
        font-size: 1.15rem;
        color: $text-primary;
        font-weight: 700;
        line-height: 1.3;
        transition: color $transition-fast;
        cursor: pointer;
        &:hover { color: $primary; }
      }
    }

    .post-excerpt {
      font-size: 0.9rem;
      color: $text-secondary;
      line-height: 1.5;
      p { margin: 0; }
    }

    footer.card-footer {
      position: absolute;
      bottom: 0;
      width: 100%;
      border-top: 1px solid $border-color;
      background: transparent;
    }

    .read-more {
      font-weight: 600;
      color: $primary !important;
      font-size: 0.9rem;
      transition: all $transition-fast;
      .arrow { transition: transform $transition-fast; display: inline-block; }
      &:hover .arrow { transform: translateX(4px); }
    }
  }
</style>
