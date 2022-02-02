<template>
  <section class="section">
    <nuxt-link to="/" class="button--green"> Home </nuxt-link>

    <nuxt-link to="/news/" class="button--green"> News </nuxt-link>
    <nuxt-link to="/about/" class="button--green"> About </nuxt-link>
    <div class="container">
      <div class="row">
        <div
          class="col-lg-4"
          v-for="(article, index) in data.articles"
          :key="index"
        >
          <a :href="article.url" target="_blank">
            <div class="card">
              <div class="card-image">
                <img :src="article.urlToImage" :alt="article.title" />
              </div>
              <div class="card-content">
                <div class="content">{{ article.title }}</div>
              </div>
            </div>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    const { data } = await $axios.get(
      `https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey=05969cc1a28143748e646d610c2c61b1`
    )

    return { data }
  },
}
</script>

<style></style>
