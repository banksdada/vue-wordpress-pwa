<template>
  <div>
    <footer class="footer">
      <div class="container">
        <div class="content has-text-centered">
          <p>
            <strong>BaseUse</strong> - Powered by WordPress &amp; Vue.js
          </p>
          <p class="is-size-7">
            Built with <a href="https://github.com/banksdada/vue-wordpress-pwa" target="_blank" rel="noopener">vue-wordpress-pwa</a>
          </p>
        </div>
      </div>
    </footer>
  </div>
</template>
<script>
  export default {
    name: "app-footer",
    data: () => {
      return {
        socialLinks: []
      };
    }
  };
</script>
