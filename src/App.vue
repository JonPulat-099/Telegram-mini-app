<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { onMounted } from 'vue'

onMounted(() => {
  // window.Telegram.WebApp.showScanQrPopup(par)
})

function showQRScanner() {
  const par = {
    text: 'Press to scan'
  }
  window.Telegram.WebApp.showScanQrPopup(par, (val) => {
    window.Telegram.WebApp.closeScanQrPopup()
    if (val) {
      window.Telegram.WebApp.PopupParams({
        title: 'Scan Res',
        message: JSON.stringify(val)
      })
    } else {
      window.Telegram.WebApp.PopupParams({
        title: 'Scan Res',
        message: 'empty'
      })
    }

    return true
  })
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <h3>QR scanner</h3>
  <button @click="showQRScanner()">Scan QR code</button><br />

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
