<template>
  <div id="app">
    <button :class="jiptEnabled && 'active' || ''" @click="handleClick">JIPT</button>
    <h1>{{ $t('message') }}</h1>
  </div>
</template>

<script>
import I18n from './i18n';

export default {
  data() {
    return {
      jiptEnabled: false,
    }
  },

  watch: {
    jiptEnabled: {
      immediate: true,
      handler() {
        this.initJipt();
      },
    }
  },

  methods: {
    handleClick() {
      this.jiptEnabled = !this.jiptEnabled;
      I18n.locale = this.jiptEnabled ? 'jipt' : 'en';
    },

    initJipt() {
      if (!this.jiptEnabled) {
        return;
      }

      window.accent = function(){(accent.q=accent.q||[]).push(arguments);}; // eslint-disable-line
      accent('init',{h:'http://localhost:4000',i:'4e150f96-0412-4bf6-937a-f54ee5cb11a3'}); // eslint-disable-line

      const scriptId = 'accent';

      const oldScript = document.querySelector(`#${scriptId}`);
      if (oldScript) {
        oldScript.remove();
      }

      let script = document.createElement('script');
      script.id = scriptId;
      script.src = 'http://localhost:4000/static/jipt/index.js';
      document.body.append(script);
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.active {
  background: gray;
}
</style>
