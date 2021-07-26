<template>
  <div id="app" class="default-transition text-high bg" :class="{ dark: dark }">
    <nav
      class="
        default-transition
        dp-00
        bg-p-500
        text-white-high text-primary-if-dark
      "
      :class="{ 'dp-04': navFixed }"
    >
      <img src="https://github.com/acedron.png" class="dp-01-shadow" alt="" />
      <h3>acedron</h3>
      <button
        @click="toggleMode"
        id="toggle-mode"
        class="dp-01-shadow bg-s-400 text-white text-primary-if-dark"
      >
        <span class="material-icons">
          {{ dark ? 'dark_mode' : 'light_mode' }}
        </span>
      </button>
    </nav>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class App extends Vue {
  dark = false;
  navFixed = false;

  created(): void {
    window.addEventListener('scroll', this.handleScroll);
  }

  destroyed(): void {
    window.removeEventListener('scroll', this.handleScroll);
  }

  handleScroll(): void {
    this.navFixed = window.scrollY > 15;
  }

  toggleMode(): void {
    this.dark = !this.dark;
  }
}
</script>

<style lang="scss">
@import 'main.scss';

#app {
  position: absolute;
  left: 0;
  top: 0;
  overflow-x: hidden;
  width: 100vw;
  min-height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/*
 * Nav
 */
#app nav {
  display: flex;
  align-items: center;
  position: fixed;
  top: 0;
  width: 100vw;
  height: 48px;
  overflow: hidden;
}

#app nav img {
  margin-left: 2%;
  margin-right: 12px;
  height: 80%;
  width: auto;
  border-radius: 8px;
}

#app nav h3 {
  display: inline-block;
}

#app nav button#toggle-mode {
  position: absolute;
  right: 2%;
  border: none;
  width: 38px;
  height: 38px;
  text-align: center;
  border-radius: 100%;
}

#app nav button#toggle-mode span {
  text-align: center;
}

/*
 * Content
 */
#content {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 60px;
  width: 100vw;
  text-align: center;
}
</style>
