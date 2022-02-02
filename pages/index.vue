<template>
  <main class="container">
    <h1 class="title">Home</h1>
    <section class="row">
      <div class="card-columns">
        <div v-for="post in currentPage" :key="post.id" class="card">
          <nuxt-link class="card-link" :to="`/news/${post.id}/`">
            <img
              v-if="post.featured_media_url"
              class="card-img-top"
              :src="post.featured_media_url"
              alt="Card image cap"
            />

            <div class="card-body">
              <h5 class="card-title" v-html="post.title.rendered" />
              <div class="card-text" v-html="post.content.rendered"></div>
              <div class="card-text" v-html="post.excerpt.rendered" />
            </div>
          </nuxt-link>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: 'HomePage',
  asyncData({ $axios }) {
    return $axios
      .get('https://veja.abril.com.br/wp-json/wp/v2/posts/?per_page=3')
      .then((currentPage) => {
        console.log('>>', currentPage)
        console.log('>>>lenght', currentPage.data.length)
        return { currentPage: currentPage.data }
      })
  },
}
</script>

<style></style>
