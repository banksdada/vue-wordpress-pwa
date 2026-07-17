<template>
  <nav class="navbar">
    <div class="navbar-brand">
      <router-link to="/category/uncategorized/" class="navbar-item">
        <img
          src="/assets/logo-horizontal.png"
          id="vwp-logo"
          alt="BaseUse"
          exact
      /></router-link>

      <div
        class="navbar-burger burger"
        data-target="navMenuColorprimary-example"
        v-on:click="toggleMenu"
      >
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>

    <div v-bind:class="{ 'navbar-menu': true, 'is-active': isMenuActive }">
      <div class="navbar-start"></div>

      <div v-bind:class="{ 'navbar-end': true, 'is-active': isMenuActive }">
        <div class="navbar-item">
          <span v-on:click="closeMenu">
            <router-link class="is-tab nav-item" to="/category/uncategorized/"
              >Blog</router-link
            >
          </span>
        </div>
        <div class="navbar-item">
          <span v-on:click="closeMenu">
            <router-link class="is-tab nav-item" to="/category/learning-paths/"
              >Learning Paths</router-link
            >
          </span>
        </div>
        <div class="navbar-item">
          <span v-on:click="closeMenu">
            <router-link class="is-tab nav-item" to="/page/about/"
              >About</router-link
            >
          </span>
        </div>
      </div>
    </div>
  </nav>
</template>
<script>
  export default {
    name: "app-header",
    data: () => {
      return {
        isMenuActive: false,
        siteName: "",
        blogItems: []
      };
    },
    methods: {
      toggleMenu() {
        this.isMenuActive = !this.isMenuActive;
      },
      closeMenu() {
        this.isMenuActive = false;
      },
      relativePath(url) {
        url = url.replace("https://", "");
        var domain = url.split("/")[0];
        return url.replace(domain, "");
      }
    }
  };
</script>
<style>
  #vwp-logo {
    max-width: 350px;
    max-height: 3rem;
  }
  #app-header .nav-menu > span > a {
    vertical-align: middle;
  }
  .nav-toggle {
    position: absolute;
    right: 0;
  }
</style>
