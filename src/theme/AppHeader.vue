<template>
  <nav class="navbar is-transparent" role="navigation">
    <div class="navbar-brand">
      <router-link to="/" class="navbar-item brand-item">
        <span class="brand-icon">BU</span>
        <span class="brand-text">BaseUse</span>
      </router-link>
      <a role="button" class="navbar-burger burger" :class="{ 'is-active': isMenuActive }" v-on:click="toggleMenu" aria-label="menu">
        <span></span><span></span><span></span>
      </a>
    </div>
    <div class="navbar-menu" :class="{ 'is-active': isMenuActive }">
      <div class="navbar-start"></div>
      <div class="navbar-end">
        <router-link class="navbar-item nav-link" to="/category/uncategorized/" v-on:click.native="closeMenu">Blog</router-link>
        <router-link class="navbar-item nav-link" to="/page/about/" v-on:click.native="closeMenu">About</router-link>
        <div class="navbar-item">
          <a class="dark-toggle" v-on:click="$emit('toggle-dark')" :title="darkMode ? 'Light mode' : 'Dark mode'">
            <span v-if="darkMode">&#9728;</span>
            <span v-else>&#9790;</span>
          </a>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'app-header',
  props: ['darkMode'],
  data () {
    return { isMenuActive: false }
  },
  methods: {
    toggleMenu () { this.isMenuActive = !this.isMenuActive },
    closeMenu () { this.isMenuActive = false }
  }
}
</script>

<style lang="scss" scoped>
  @import '../variables';

  .navbar {
    background: rgba(255, 255, 255, 0.9) !important;
    backdrop-filter: blur(20px);
    box-shadow: 0 1px 3px rgba(0,0,0,0.06);
    padding: 0.5rem 1rem;
    transition: all $transition-smooth;
  }

  .brand-item {
    padding: 0.5rem 1rem;
  }

  .brand-icon {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 36px;
    height: 36px;
    background: linear-gradient(135deg, $gradient-start, $gradient-end);
    color: white;
    border-radius: 10px;
    font-weight: 800;
    font-size: 0.85rem;
    margin-right: 0.5rem;
  }

  .brand-text {
    font-weight: 700;
    font-size: 1.25rem;
    color: $text-primary;
    letter-spacing: -0.5px;
  }

  .nav-link {
    font-weight: 500;
    transition: color $transition-fast;
    &:hover {
      color: $primary !important;
    }
  }

  .dark-toggle {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background: linear-gradient(135deg, #2d3436, #636e72);
    color: white;
    font-size: 1.1rem;
    cursor: pointer;
    transition: transform $transition-fast;
    &:hover { transform: rotate(20deg) scale(1.1); }
  }
</style>
