<template>
  <div class="container">
    <header class="header d-flex flex-column">
      <h1 class="title">News</h1>

      <div class="d-flex justify-content-between align-items-center">
        <button
          class="button--grey"
          :disabled="pageNumber === 0"
          @click="prevPage"
        >
          Prev
        </button>

        <span>{{ pageNumber + 1 }}/{{ pageCount }}</span>

        <button
          class="button--grey"
          :disabled="pageNumber >= pageCount - 1"
          @click="nextPage"
        >
          Next
        </button>
      </div>
    </header>

    <hr />

    <section class="row">
      <div class="card-columns">
        <div v-for="post in paginatedData" :key="post.id" class="card">
          <nuxt-link class="card-link" :to="`/news/${post.id}/`">
            <img
              v-if="post.featured_media_url"
              class="card-img-top"
              :src="post.featured_media_url"
              alt="Card image cap"
            />

            <div class="card-body">
              <h5 class="card-title" v-html="post.title.rendered" />

              <div class="card-text" v-html="post.excerpt.rendered" />
            </div>
          </nuxt-link>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'News',
  data() {
    return {
      pageNumber: 0,
      perPage: 9,
    }
  },
  computed: {
    pageCount() {
      const l = this.currentPage.length
      const s = this.perPage

      return Math.ceil(l / s)
    },
    paginatedData() {
      const start = this.pageNumber * this.perPage
      const end = start + this.perPage

      return this.currentPage.slice(start, end)
    },
  },
  asyncData({ $axios }) {
    return $axios
      .get('https://veja.abril.com.br/wp-json/wp/v2/posts/?per_page=90')
      .then((currentPage) => {
        return {
          currentPage: currentPage.data,
        }
      })
  },
  methods: {
    changePage(event) {
      this.pageNumber = event.target.value - 1
    },
    nextPage() {
      this.pageNumber++
    },
    prevPage() {
      this.pageNumber--
    },
  },
}
</script>

<style scoped>
</style>
