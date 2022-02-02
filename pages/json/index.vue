<template>
  <main>
    <div class="container">
      <div class="row">
        <h1 class="title">JSON</h1>

        <div class="col-12 d-flex flex-wrap">
          <!-- Single starts -->
          <div
            v-for="(items, index) in pageData.home"
            :key="index"
            class="col-md-4"
          >
            <div class="item">
              <div class="image">
                <img src="https://images.unsplash.com/photo-1438761681033-6461ffad8d80?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80" />
                <div class="buttons">
                  <a href="#"><i class="fa fa-facebook"></i></a>
                  <a href="#"><i class="fa fa-twitter"></i></a>
                  <a href="#"><i class="fa fa-instagram"></i></a>
                </div>
              </div>
              <a class="name" href="#">{{ items.name }}</a>
              <p class="desc">
                {{ items.about }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    try {
      const pageData = await $content('home').fetch()
      return { pageData }
    } catch (e) {
      console.error(e)
      return error({ statusCode: 404, message: e })
    }
  },
}
</script>

<style>
.item a {
  text-decoration: none;
}
.item .image {
  position: relative;
  overflow: hidden;
  margin-bottom: 40px;
}
.item .image img {
  transition: all 0.2s;
  height: 300px;
  object-fit: cover;
}
.buttons {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  opacity: 0;
  visibility: hidden;
  background-color: rgba(255, 255, 255, 0);
  transition: all 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
}
.item .image .buttons a {
  color: #fff;
  margin-right: 10px;
}
.item .image .buttons a:last-child {
  margin-right: 0;
}
.item .image .buttons a i {
  font-size: 20px;
  color: inherit;
}
.item .image:hover .buttons {
  opacity: 1;
  visibility: visible;
  background-color: rgba(39, 48, 75, 0.7);
}
.item .image:hover img {
  transform: scale(1.1);
}
.item {
  background: #fff;
  padding: 15px;
  text-align: center;
  transition: all 0.3s ease;
  border: 3px solid transparent;
  box-shadow: 0 0 16px 0 rgba(39, 48, 75, 0.15);
  border-radius: 6px;
  padding: 35px 30px 27px;
  display: flex;
  flex-direction: column;
}
.item img {
  max-width: 100%;
}
.item h2 {
  color: #5a3733;
  font-size: 22px;
  font-weight: 900;
  padding: 0.5em 0;
  margin: 0;
}
.item p {
  font-size: 14px;
  line-height: 1.5em;
  margin: 14px 0 20px;
}
.item .name {
  font-size: 24px;
  text-transform: capitalize;
  transition: all 0.3s linear 0s;
  font-weight: 700;
  line-height: 1;
  color: #27304b;
}
.item .name:hover {
  color: #f15e42;
}
.item .perUnvan {
  position: relative;
  transition: all 0.3s linear 0s;
  color: #777;
  font-size: 16px;
  text-align: center;
  font-weight: 400;
}
.item .perUnvan:hover {
  color: #f15e42;
}
.item .perUnvan::after {
  content: '';
  position: absolute;
  bottom: -6px;
  left: 50%;
  height: 1px;
  width: 40px;
  background-color: #777;
  transform: translateX(-50%);
}
.item .css-arrow {
  margin-left: 10px;
  display: inline-block;
  width: 55px;
  height: 2px;
  background-color: #f15e42;
  position: relative;
  transition: all 0.25s linear 0s;
  vertical-align: middle;
}
.item .css-arrow::after {
  content: '';
  position: absolute;
  width: 10px;
  height: 2px;
  background-color: #f15e42;
  top: -3px;
  right: -3px;
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
  transition: all 0.25s linear 0;
}
.item .css-arrow::before {
  content: '';
  position: absolute;
  width: 10px;
  height: 2px;
  background-color: #f15e42;
  top: 3px;
  right: -3px;
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
  transition: all 0.25s linear 0;
}
.item .read-more {
  font-size: 16px;
  font-weight: 700;
  text-transform: capitalize;
  color: #27304b;
  position: relative;
  margin-top: 20px;
}
.item .read-more:hover {
  color: #f15e42;
}
.item:hover .css-arrow {
  width: 20px;
}
</style>
