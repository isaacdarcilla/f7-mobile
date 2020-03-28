<template>
  <f7-page no-toolbar no-navbar no-swipeback login-screen>
    <f7-block>
      <div>
        <center>
          <img
            style="padding-top: 50px;"
            slot="media"
            src="../../assets-src/pancake.png"
            height="90"
            width="90"
          />
        </center>
        <f7-login-screen-title><b>DesktopQA</b></f7-login-screen-title>
      </div>
    </f7-block>
    <form v-on:submit.prevent="onLogin" action="" method="GET">
      <f7-list class="login-list">
        <f7-list-input
          label="Email Address"
          type="email"
          placeholder="Enter your email address"
          :value="email"
          @input="email = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>
        <f7-list-input
          label="Password"
          type="password"
          placeholder="Enter your password"
          :value="password"
          @input="password = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>
      </f7-list>
      <f7-block>
        <f7-list>
          <f7-button type="submit"><b>Sign In</b></f7-button>
          <f7-block-footer
            >Desktop Query developed by &copy Isaac</f7-block-footer
          >
        </f7-list>
      </f7-block>
    </form>
  </f7-page>
</template>
<script>
import md5 from "md5.js";
import $ from "jquery";

export default {
  data() {
    return {
      user: null,
      authenticate: [],
      email: "",
      password: ""
    };
  },

  methods: {
    onLogin() {
      const self = this;
      const app = self.$f7;
      const router = self.$f7router;

      var encrypt = new md5();
      encrypt.end(this.password);
      var encrypted = encrypt.read().toString("hex");

      var api =
        "https://querybackend.herokuapp.com/login-with-email.php?email=" +
        this.email +
        "&password=" +
        encrypted;

      console.log(encrypted);
      console.log(api);

      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        success: function(data) {
          self.authenticate = data;

          if (self.authenticate == "true") {
            console.log(data);
            router.navigate("/home");
          } else {
            app.dialog.alert(
              "Username or password is incorrect.",
              "Login Failed"
            );
            console.log(data);
          }
        }
      });
    }
  },

  mounted() {}
};
</script>
