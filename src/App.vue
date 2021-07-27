<template>
  <div id="app" class="default-transition bg" :class="{ dark: dark }">
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
        class="
          default-transition
          dp-01-shadow
          bg-s-400
          text-white-high text-primary-if-dark
          tr-button-scale
        "
      >
        <span class="material-icons">
          {{ dark ? 'dark_mode' : 'light_mode' }}
        </span>
      </button>
    </nav>

    <section id="content" class="default-transition text-high">
      <h1>test</h1>
      <img
        src="https://github.com/acedron.png"
        height="1024"
        class="dp-01-shadow"
        alt=""
      />
    </section>

    <transition name="fade">
      <div
        id="cookie-notice"
        v-if="dismissedCookieNotice === false"
        class="dp-04-shadow bg-p-500 text-white-high"
      >
        <h4 class="text-white-high">
          This site uses cookies and/or HTML5 local storage for additional
          functionality such as saving options. By clicking "Allow", you agree
          to the storing of cookies or data on your device to enhance site
          navigation and provide more functionality. No data will be stored
          until you allow.
        </h4>
        <button
          @click="cookieNoticeDismiss($event, false)"
          class="
            default-transition
            dp-01-shadow
            bg-s-600
            text-white-high text-primary-if-dark
            tr-button-scale
          "
        >
          Deny
        </button>
        <button
          @click="cookieNoticeDismiss($event, true)"
          class="
            default-transition
            dp-01-shadow
            bg-s-600
            text-white-high text-primary-if-dark
            tr-button-scale
          "
        >
          Allow
        </button>
      </div>
    </transition>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class App extends Vue {
  dark = false;
  navFixed = false;
  dismissedCookieNotice = false;

  mounted(): void {
    window.addEventListener('scroll', this.handleScroll);

    if (localStorage.dismissedCookieNotice)
      this.dismissedCookieNotice =
        localStorage.dismissedCookieNotice === 'true';

    if (localStorage.dark) this.dark = localStorage.dark === 'true';
  }

  unmounted(): void {
    window.removeEventListener('scroll', this.handleScroll);
  }

  handleScroll(): void {
    this.navFixed = window.scrollY > 48;
  }

  toggleMode(): void {
    this.dark = !this.dark;
    if (localStorage.acceptedCookies && localStorage.acceptedCookies === 'true')
      localStorage.dark = this.dark;
  }

  cookieNoticeDismiss(_event: Event, accepted: boolean): void {
    localStorage.dismissedCookieNotice = true;
    localStorage.acceptedCookies = accepted;
    this.dismissedCookieNotice = true;
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
 * Cookie Notice
 */

#cookie-notice {
  display: flex;
  position: fixed;
  align-items: center;
  bottom: 0;
  width: 100vw;
  height: 48px;
  z-index: 70;
  overflow: hidden;
}

#cookie-notice h4 {
  margin-left: 16px;
  height: 100%;
  overflow-y: auto;
  white-space: normal;
  border-radius: 4px;
  border: none;
}

#cookie-notice button {
  border: none;
  margin-right: 16px;
  width: 128px;
  height: 32px;
  border-radius: 4px;
  font-weight: 600;
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
  overflow-x: hidden;
}

/*
 * Vue Transitions
 */
.fade-enter-active,
.fade-leave-active {
  transition: all 0.15s ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
