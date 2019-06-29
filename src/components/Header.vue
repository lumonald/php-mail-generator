<template>
  <b-row class="d-flex justify-content-center pt-3">
    <Heading/>
    <Intro/>
  </b-row>
</template>
<script>
import Heading from "../components/Heading.vue";
import Intro from "../components/Intro.vue";

export default {
  name: "header",
  components: {
    Heading,
    Intro
  }
};
</script>
