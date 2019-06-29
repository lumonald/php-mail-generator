<template>
  <div id="app">
    <b-container>
      <Header />
      <b-row class="d-flex justify-content-center">
        <b-col sm="9">
          <Generator />
        </b-col>
      </b-row>
    </b-container>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Generator from "./components/Generator.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "app",
  components: {
    Header,
    Generator,
    Footer
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Hind+Madurai&display=swap");
@import "assets/scss/global.scss";

#app {
  height: 100vh;
  min-height: 100%;
  display: grid;
  grid-template-rows: auto 45px;
  text-shadow: 0 -1px 0 $dark_grey;
}

p span {
  background: $dark_grey;
  color: $text_colour;
  font-family: $font;
  border-radius: 0.25rem;
  padding: 0.1em 0.4em;
  font-size: 0.9em;
}

@media (min-width: 576px) {
  #intro {
    text-align: right;
  }
}

.input-group-prepend {
  text-shadow: none;
}
</style>
