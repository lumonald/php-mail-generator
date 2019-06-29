<template>
  <b-col sm="4" class="pt-3" id="intro">
    <p>
      Quickly generate basic PHP
      <span>mail()</span> code online.
    </p>
    <b-modal ok-only id="modal-1" title="About">
      <p class="my-4">
        This tool conveniently generates code to send an email in PHP. It ensures the required headers are present to get you started, but does not include all of the available options for the PHP mail() function. For more options and other headers available, see the
        <a href="https://www.php.net/manual/en/function.mail.php">PHP manual</a>.
      </p>
    </b-modal>
  </b-col>
</template>

<script>
export default {
  name: "intro"
};
</script>
<style>
#intro {
  text-align: left;
}
</style>
