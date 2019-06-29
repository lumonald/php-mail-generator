<template>
  <b-container fluid class="footer">
    <b-row>
      <b-col>
        <b-button v-b-modal.modal-1>
          <font-awesome-icon icon="info" fixed-width />
        </b-button>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: "footer"
};
</script>
<style lang="scss">
@import "../assets/scss/global.scss";
@import "~bootstrap/scss/functions";
@import "~bootstrap/scss/variables";
@import "~bootstrap/scss/mixins";

.footer {
  grid-row-start: 2;
  grid-row-end: 2;
  color: $text_colour;
}

#modal-1 {
  color: $dark_grey;
}

.btn-primary {
  @include button-variant(
    $main_colour,
    darken($main_colour, 7.5%),
    darken($main_colour, 10%),
    lighten($main_colour, 5%),
    lighten($main_colour, 10%),
    darken($main_colour, 30%)
  );
}

.btn-outline-primary {
  @include button-outline-variant(
    $main_colour,
    #222222,
    lighten($main_colour, 5%),
    $main_colour
  );
}
</style>
