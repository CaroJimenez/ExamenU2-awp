<template>
  <div class="main">
    <div class="carousel" v-show="showElement">
      <b-carousel
        id="carousel-1"
        v-model="slide"
        :interval="4000"
        controls
        indicators
        background="#ababab"
        img-width="1024"
        img-height="480"
        style="text-shadow: 1px 1px 2px #333"
        @sliding-start="onSlideStart"
        @sliding-end="onSlideEnd"
      >
        <b-carousel-slide
          caption="First slide"
          text="Nulla vitae elit libero, a pharetra augue mollis interdum."
          img-src="https://picsum.photos/1024/480/?image=52"
        ></b-carousel-slide>

        <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=54">
          <h1>Hello world!</h1>
        </b-carousel-slide>

        <!-- Slides with image only -->
        <b-carousel-slide
          img-src="https://picsum.photos/1024/480/?image=58"
        ></b-carousel-slide>

        <!-- Slides with img slot -->
        <!-- Note the classes .d-block and .img-fluid to prevent browser default image alignment -->
        <b-carousel-slide>
          <template #img>
            <img
              class="d-block img-fluid w-100"
              width="1024"
              height="480"
              src="https://picsum.photos/1024/480/?image=55"
              alt="image slot"
            />
          </template>
        </b-carousel-slide>
      </b-carousel>
    </div>

    <div class="bodyContainer">
      <div class="filtersAndButton">
        <b-button variant="primary" @click="openModal"
          >Ordenar por autor</b-button
        >
        <b-button variant="primary" @click="openModal"
          >Ordenar por fecha</b-button
        >
        <b-button variant="primary" @click="openModal"
          >Mostrar si tiene imagen</b-button
        >
        <AddBook />
      </div>
      <Cards />
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import AddBook from "../components/AddBook.vue";
import Cards from "../components/Cards.vue";
export default Vue.extend({
  components: {
    AddBook,
    Cards,
  },
  data() {
    return {
      showElement: true,
      lastScrollPosition: 0,
    };
  },
  mounted() {
    window.addEventListener("scroll", this.onScroll);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.onScroll);
  },
  methods: {
    onScroll() {
      const currentScrollPosition =
        window.pageYOffset || document.documentElement.scrollTop;
      if (Math.abs(currentScrollPosition - this.lastScrollPosition) < 60) {
        return;
      }
      this.showElement = currentScrollPosition < this.lastScrollPosition;
      this.lastScrollPosition = currentScrollPosition;
    },
    onSlideStart(slide) {
      this.sliding = true;
    },
    onSlideEnd(slide) {
      this.sliding = false;
    },
  },
});
</script>

<style>
.main {
  display: flex;
  flex-direction: column;
}

.bodyContainer {
  min-height: 960px;
}

.filtersAndButton {
  display: flex;
  flex-wrap: wrap;
  padding: 1%;
  justify-content: space-between;
  margin-top: 1%;
  margin-right: 15%;
  margin-left: 15%;
}
</style>
