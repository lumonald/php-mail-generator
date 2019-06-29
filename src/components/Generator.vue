<template>
  <div class="mt-1">
    <b-row>
      <b-col sm="12">
        <b-input-group prepend="From">
          <b-form-input
            :value="fromEmail"
            @change.native="fromEmail = $event.target.value"
            type="text"
            name="fromEmail"
            placeholder="Email *"
          ></b-form-input>
          <b-form-input v-model="fromName" type="text" name="fromName" placeholder="Name"></b-form-input>
        </b-input-group>
        <span class="error" v-if="!$v.fromEmail.email">Ensure you use a valid email address</span>
        <b-input-group prepend="To" class="mt-2">
          <b-form-input
            :value="toEmail"
            @change.native="toEmail = $event.target.value"
            type="text"
            name="toEmail"
            placeholder="Email *"
          ></b-form-input>
          <b-form-input v-model="toName" type="text" name="toName" placeholder="Name"></b-form-input>
        </b-input-group>
        <span class="error" v-if="!$v.toEmail.email">Ensure you use a valid email address</span>
        <b-input-group prepend="Anyone else?" class="mt-2">
          <b-form-input
            :value="cc"
            @change.native="cc = $event.target.value"
            type="text"
            name="cc"
            placeholder="Cc"
          ></b-form-input>
          <b-form-input
            :value="bcc"
            @change.native="bcc = $event.target.value"
            type="text"
            name="bcc"
            placeholder="Bcc"
          ></b-form-input>
        </b-input-group>
        <span class="error" v-if="!$v.cc.email">Ensure you use a valid email address for the Cc</span>
        <span class="error" v-if="!$v.bcc.email">Ensure you use a valid email address for the Bcc</span>
        <b-input-group prepend="Other" class="mt-2">
          <b-form-input v-model="subject" type="text" name="subject" placeholder="Subject *"></b-form-input>
          <b-form-input
            :value="replyToEmail"
            @change.native="replyToEmail = $event.target.value"
            type="text"
            name="replyToEmail"
            placeholder="Reply To"
          ></b-form-input>
        </b-input-group>
        <span
          class="error"
          v-if="!$v.replyToEmail.email"
        >Ensure you use a valid email address for the Reply To</span>
        <div class="mt-2">
          <b-form-textarea
            id="textarea"
            v-model="message"
            placeholder="Enter a message..."
            rows="2"
            max-rows="2"
            maxlength="70"
            @keydown.enter.exact.prevent
          ></b-form-textarea>
        </div>
        <div class="mt-2">
          <label class="radio-inline">
            <b-form-radio
              type="radio"
              v-model="type"
              name="type"
              value="html"
              class="mr-3"
              checked
            >HTML</b-form-radio>
          </label>
          <label class="radio-inline">
            <b-form-radio type="radio" v-model="type" name="type" value="plain">Plain text</b-form-radio>
          </label>
        </div>
      </b-col>
    </b-row>

    <b-row>
      <b-col sm="12">
        <div class="output mt-1">
          <div>$to = "{{ spaced(toName) }}{{ formatEmail(toEmail, toName) }}";</div>
          <div>$subject = "{{ subject }}";</div>
          <div>$message = "{{ message }}";</div>
          <div>$headers = "From: {{ spaced(fromName) }}{{ formatEmail(fromEmail, fromName) }}\r\n";</div>
          <div>$headers .= "MIME-Version: 1.0\r\n";</div>
          <div v-if="cc">{{ insertHeader(cc, 'Cc') }}</div>
          <div v-if="bcc">{{ insertHeader(bcc, 'Bcc') }}</div>
          <div v-if="replyToEmail">{{ insertHeader(replyToEmail, 'Reply-to') }}</div>
          <div>$headers .= "Content-Type: text/{{ type }}; charset=UTF-8\r\n";</div>
          <div>
            <br />mail($to, $subject, $message, $headers);
          </div>
        </div>
      </b-col>
    </b-row>
  </div>
</template>

<script>
const { required, email, maxLength } = require("vuelidate/lib/validators");
export default {
  name: "generator",
  data: () => {
    return {
      fromEmail: "",
      fromName: "",
      toEmail: "",
      toName: "",
      cc: "",
      bcc: "",
      subject: "",
      replyToEmail: "",
      message: "",
      type: "html",
      output: ""
    };
  },
  validations: {
    fromEmail: {
      required,
      email
    },
    toEmail: {
      email
    },
    cc: {
      email
    },
    bcc: {
      email
    },
    replyToEmail: {
      email
    },
    message: {
      maxLength: maxLength(70)
    }
  },
  methods: {
    formatEmail: (email, name) => {
      if (name && email) {
        return "<" + email + ">";
      } else {
        return email;
      }
    },
    insertHeader: (value, type) => {
      return '$headers .= "' + type + ": " + value + '\\r\\n";';
    },
    insertNewline: values => {
      if (values[0]) return '\\r\\n";';
    },
    spaced: value => {
      if (value) return value + " ";
    }
  }
};
</script>

<style lang="scss">
@import "../assets/scss/global.scss";
.output {
  background: $dark_grey;
  color: $text_colour;
  font-family: $font_code;
  padding: 2em;
  border-radius: 0.25rem;
  overflow-x: scroll;
}

span.error {
  font-size: 0.8em;
  background: $bg_error;
  padding: 0.1em 0.7em;
  border-radius: 3px;
  margin-top: 0.5em;
  margin-right: 0.5em;
  border: 2px solid $border_error;
  display: inline-block;
}
</style>
