<template>
  <main class="container">
    <header class="header d-flex flex-column">
      <div class="links">
        <nuxt-link to="/" class="button--green p-2"> Home </nuxt-link>

        <nuxt-link to="/news/" class="button--green p-2"> News </nuxt-link>
        <nuxt-link to="/programs-api/" class="button--green p-2"> Programs-API </nuxt-link>
        <nuxt-link to="/json/" class="button--green p-2"> JSON </nuxt-link>
      </div>
    </header>
  </main>
</template>

<script>
export default {
  name: 'BaseHeader',
}
</script>

<style>
.header {
  align-items: center;
  justify-content: center;
  margin: 2rem auto;
  text-align: center;
}
.links {
  padding-top: 15px;
}
</style>
