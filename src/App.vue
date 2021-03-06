<template>
  <div id="app">
    <header>
      <router-link to="/">
        <h1><em>PELLE LINDROTH</em></h1>
      </router-link>

      <nav>
        <router-link to="/projects">{{ $t('menu.projects') }}</router-link>
        <router-link to="/cv">{{ $t('menu.about') }}</router-link>
        <router-link to="/contact">{{ $t('menu.contact') }}</router-link>
      </nav>
      <img class="flag" @click="changeLocale" :src="getFlagIcon" alt="" />
    </header>
    <router-view />
    <footer>
      <p>© Pelle Lindroth 2021</p>
    </footer>
  </div>
</template>

<script>
export default {
  computed: {
    getFlagIcon() {
      return require(`@/assets/icons/lang-${this.flag}-icon.png`)
    },
  },
  data() {
    return {
      flag: 'en',
      sv: true,
    }
  },
  methods: {
    changeLocale() {
      this.sv = !this.sv
      this.flag = this.sv ? 'en' : 'sv'
      this.$root.$i18n.locale = this.sv ? 'sv' : 'en'
    },
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Monoton&family=Kanit:wght@700&family=Roboto:ital,wght@0,300;0,400;0,700;0,900;1,300&display=swap');
$mobile-cutoff: 650px;

:root {
  font-size: 10px;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: #333;
  height: 100vh;
}

#app {
  color: #ececec;
  cursor: default;
  font-family: 'Roboto', sans-serif;
  padding: 0 2rem;
  -webkit-font-smoothing: antialiased;

  @media screen and (max-width: $mobile-cutoff) {
    padding: 0;
  }

  header {
    align-items: center;
    border-bottom: 1px solid #fcd577;
    display: flex;
    height: 7.7rem;
    justify-content: space-between;
    margin: 2rem auto 0;
    max-width: 120rem;
    padding: 0 0 2rem;

    @media screen and (max-width: $mobile-cutoff) {
      height: 6rem;
      margin: 0 auto;
      width: 100%;
      padding: 0 1rem;
    }

    a {
      align-items: baseline;
      display: flex;
      min-width: 30%;
      text-decoration: none;
    }

    h1 {
      color: #fcd577;
      font-family: 'Kanit', sans-serif;
      font-size: 4rem;
      font-weight: 700;
      letter-spacing: 1.3px;
      text-decoration: none;
      text-shadow: 0 0 1rem #fcd577;

      @media screen and (max-width: $mobile-cutoff) {
        font-size: 2rem;
        letter-spacing: 0.2px;
      }
    }

    .flag {
      border-radius: 50%;
      box-shadow: 0 0 0.5rem rgba(255, 255, 255, 0.5);
      cursor: pointer;
      margin-left: 1rem;
      width: 2.5rem;

      @media screen and (max-width: $mobile-cutoff) {
        margin-left: 0;
        width: 1.5rem;
      }
    }

    nav {
      align-items: center;
      display: flex;
      justify-content: space-between;
      margin-left: auto;
      min-width: 30rem;

      @media screen and (max-width: $mobile-cutoff) {
        margin-left: 0;
        min-width: 15rem;
      }

      a {
        color: #fcd577;
        font-size: 1.8rem;
        font-weight: 700;
        text-align: center;
        text-decoration: none;

        @media screen and (max-width: $mobile-cutoff) {
          font-size: 1.2rem;
        }
      }

      .router-link-active {
        border-radius: 0.5rem;
        color: #fcd577;
        text-shadow: 1px 1px 30px #fff;
      }
    }
  }

  footer {
    background-color: rgba(255, 2555, 255, 0.1);
    display: grid;
    height: 8rem;
    margin-left: -2rem;
    place-items: center;
    width: 100vw;

    @media screen and (max-width: $mobile-cutoff) {
      height: 6rem;
      margin-left: 0;
    }

    p {
      color: #fcd577;
      font-size: 1.5rem;
      font-weight: 700;

      @media screen and (max-width: $mobile-cutoff) {
        font-size: 1.2rem;
        font-weight: 500;
      }
    }
  }
}
</style>
