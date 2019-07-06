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
          <div>
            $to = "<span v-if="toName">
              <span v-dompurify-html="toName"></span>
            </span>
            <span v-if="toName && toEmail">&nbsp;&lt;</span>
            <span v-if="toEmail">
              <span v-dompurify-html="toEmail"></span>
              <span v-if="toName && toEmail">&gt;</span>
            </span>";
          </div>
          <div>
            $subject = "<span v-dompurify-html="subject"></span>";
          </div>
          <div>
            $message = "<span v-dompurify-html="message"></span>";
          </div>
          <div>
            $headers = "From: <span v-if="fromName">
              <span v-dompurify-html="fromName"></span>
            </span>
            <span v-if="fromName && fromEmail">&nbsp;&lt;</span>
            <span v-if="fromEmail">
              <span v-dompurify-html="fromEmail"></span>
              <span v-if="fromName && fromEmail">&gt;</span>
            </span>\r\n";
          </div>
          <div>$headers .= "MIME-Version: 1.0\r\n";</div>
          <div v-if="cc">$headers .= "Cc: <span v-dompurify-html="cc"></span>\r\n";</div>
          <div v-if="bcc">$headers .= "Bcc: <span v-dompurify-html="bcc"></span>\r\n";</div>
          <div v-if="replyToEmail">$headers .= "Reply-to: <span v-dompurify-html="replyToEmail"></span>\r\n";</div>                    
          <div>$headers .= "Content-Type: text/<span v-dompurify-html="type"></span>; charset=UTF-8\r\n";</div>
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
    }, 
    subject: {
      maxLength: maxLength(70)
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
