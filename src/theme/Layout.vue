<template>
  <div id="app" :class="{ 'dark-mode': darkMode }">
    <app-header :darkMode="darkMode" @toggle-dark="darkMode = !darkMode"></app-header>
    <section class="hero-section" v-if="$route.path === '/' || $route.path === '/category/uncategorized/'">
      <div class="hero-bg">
        <div class="floating-shape shape-1"></div>
        <div class="floating-shape shape-2"></div>
        <div class="floating-shape shape-3"></div>
        <div class="floating-shape shape-4"></div>
        <div class="floating-shape shape-5"></div>
      </div>
      <div class="hero-content">
        <h1 class="hero-title">BaseUse</h1>
        <p class="hero-subtitle">Your digital workspace, powered by WordPress &amp; Vue.js</p>
        <div class="hero-divider"></div>
      </div>
    </section>
    <section class="main-section section">
      <div class="container content">
        <router-view></router-view>
      </div>
    </section>
    <app-footer></app-footer>
  </div>
</template>

<script>
import AppHeader from './AppHeader.vue'
import AppFooter from './AppFooter.vue'

export default {
  name: 'app',
  components: {
    'app-header': AppHeader,
    'app-footer': AppFooter
  },
  data () {
    return {
      darkMode: false
    }
  },
  watch: {
    darkMode (val) {
      localStorage.setItem('darkMode', val)
    }
  },
  mounted () {
    this.darkMode = localStorage.getItem('darkMode') === 'true'
  }
}
</script>

<style lang="scss">
  @import '../_variables';
  @import '~bulma';
  @import '../assets/fontello/css/fontello.css';

  * { box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Segoe UI', -apple-system, BlinkMacSystemFont, sans-serif;
    -webkit-font-smoothing: antialiased;
  }

  #app {
    min-height: 100vh;
    transition: background-color $transition-smooth, color $transition-smooth;
    background-color: $background;
    color: $text-primary;
  }

  #app.dark-mode {
    background-color: $dark-bg;
    color: $dark-text;
    .main-section { background-color: $dark-bg; }
    .card { background: $dark-card; color: $dark-text; border: 1px solid rgba(255,255,255,0.05); }
    .navbar { background: rgba(10, 10, 26, 0.95) !important; backdrop-filter: blur(20px); }
    .navbar-item, .navbar-link { color: $dark-text !important; }
    .footer { background: $dark-card !important; color: $dark-text !important; }
    .footer a { color: $accent-light !important; }
    h1, h2, h3, h4 { color: $dark-text; }
  }

  .main-section {
    background-color: $background;
    min-height: 600px;
    padding: 2rem 0;
  }

  .hero-section {
    position: relative;
    overflow: hidden;
    background: linear-gradient(135deg, $gradient-start, $gradient-mid, $gradient-end);
    padding: 4rem 2rem;
    text-align: center;
    color: white;
    min-height: 280px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .hero-bg {
    position: absolute;
    top: 0; left: 0; right: 0; bottom: 0;
    overflow: hidden;
  }

  .floating-shape {
    position: absolute;
    border-radius: 50%;
    opacity: 0.15;
    background: white;
  }

  .shape-1 { width: 200px; height: 200px; top: -50px; left: 10%; animation: float1 8s ease-in-out infinite; }
  .shape-2 { width: 120px; height: 120px; top: 60%; right: 15%; animation: float2 10s ease-in-out infinite; }
  .shape-3 { width: 80px; height: 80px; bottom: 10%; left: 30%; animation: float3 7s ease-in-out infinite; }
  .shape-4 { width: 150px; height: 150px; top: 20%; right: 30%; animation: float1 12s ease-in-out infinite reverse; }
  .shape-5 { width: 60px; height: 60px; top: 40%; left: 5%; animation: float2 9s ease-in-out infinite; }

  @keyframes float1 {
    0%, 100% { transform: translateY(0) rotate(0deg); }
    50% { transform: translateY(-30px) rotate(10deg); }
  }
  @keyframes float2 {
    0%, 100% { transform: translateY(0) translateX(0); }
    50% { transform: translateY(-20px) translateX(15px); }
  }
  @keyframes float3 {
    0%, 100% { transform: translateY(0) scale(1); }
    50% { transform: translateY(-25px) scale(1.1); }
  }

  .hero-content {
    position: relative;
    z-index: 2;
    animation: fadeInUp 0.8s ease-out;
  }

  @keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .hero-title {
    font-size: 3.5rem;
    font-weight: 800;
    margin-bottom: 0.5rem;
    letter-spacing: -1px;
    text-shadow: 0 2px 10px rgba(0,0,0,0.2);
  }

  .hero-subtitle {
    font-size: 1.25rem;
    opacity: 0.9;
    font-weight: 300;
    max-width: 500px;
    margin: 0 auto;
  }

  .hero-divider {
    width: 60px;
    height: 3px;
    background: rgba(255,255,255,0.6);
    margin: 1.5rem auto 0;
    border-radius: 2px;
  }

  .vwp-loading { text-align: center; }

  .fake-card {
    min-height: 300px;
    background: linear-gradient(135deg, #f0f0f0 25%, #e8e8e8 50%, #f0f0f0 75%);
    background-size: 200% 100%;
    animation: shimmer 1.5s ease-in-out infinite;
    border-radius: $radius;
  }

  @keyframes shimmer {
    0% { background-position: 200% 0; }
    100% { background-position: -200% 0; }
  }

  .fake-single-content { min-height: 500px; }
  .is-fullwidth { width: 100%; }
  .display-inline { display: inline-block; }

  .control { position: relative; text-align: left; }
  .control.is-grouped > .control.is-expanded { flex-grow: 1; flex-shrink: 1; }
  .control.is-grouped > .control:not(:last-child) { margin-bottom: 0; margin-right: .75rem; }
  .control.is-grouped { display: flex; justify-content: flex-start; }
  .control.is-grouped > .control { flex-basis: 0; flex-shrink: 0; }

  .clearfix { clear: both; }
</style>
