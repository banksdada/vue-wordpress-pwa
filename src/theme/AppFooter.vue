<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-brand">
          <span class="footer-logo">BU</span>
          <div>
            <strong>BaseUse</strong>
            <p class="footer-tagline">Your digital workspace</p>
          </div>
        </div>
        <div class="footer-links">
          <a href="https://github.com/banksdada/vue-wordpress-pwa" target="_blank" rel="noopener">GitHub</a>
          <a href="/wp-json/" target="_blank">REST API</a>
          <a href="/wp-admin/" target="_blank">Admin</a>
        </div>
        <div class="footer-bottom">
          <p>Built with WordPress &amp; Vue.js PWA</p>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'app-footer'
}
</script>

<style lang="scss" scoped>
  @import '../variables';

  .footer {
    background: linear-gradient(135deg, #2d3436, #1a1a2e) !important;
    color: rgba(255,255,255,0.7);
    padding: 2.5rem 1.5rem;
    margin-top: 3rem;
  }

  .footer-content {
    max-width: 800px;
    margin: 0 auto;
    text-align: center;
  }

  .footer-brand {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.75rem;
    margin-bottom: 1.5rem;
    strong { color: white; font-size: 1.1rem; }
  }

  .footer-logo {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    background: linear-gradient(135deg, $gradient-start, $gradient-end);
    color: white;
    border-radius: 10px;
    font-weight: 800;
    font-size: 0.9rem;
  }

  .footer-tagline {
    font-size: 0.8rem;
    opacity: 0.6;
    margin: 0.15rem 0 0;
  }

  .footer-links {
    display: flex;
    justify-content: center;
    gap: 2rem;
    margin-bottom: 1.5rem;
    a {
      color: rgba(255,255,255,0.6) !important;
      font-size: 0.9rem;
      transition: color $transition-fast;
      &:hover { color: $accent-light !important; }
    }
  }

  .footer-bottom {
    border-top: 1px solid rgba(255,255,255,0.1);
    padding-top: 1rem;
    p { font-size: 0.8rem; opacity: 0.5; margin: 0; }
  }
</style>
