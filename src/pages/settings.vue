<template>
  <f7-page name="settings">
    <f7-navbar title="Account Setting"></f7-navbar>
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
      </div>
    </f7-block>    
    <f7-block>
      <f7-list>
        <f7-block-footer
          ><center>Desktop Query for Management Information Services designed and developed by <a href="https://www.facebook.com/isaacdarcilla" target="_blank">Isaac</a></center>         
        </f7-block-footer>
        <p><center>
          Version 7.8.2016 (marga)
        </center></p>
      </f7-list>
      <f7-button v-on:click="onLogoutClicked" color="red"><b>Logout</b></f7-button>      
    </f7-block>
  </f7-page>
</template>

<script>

export default {
  methods: {
    onLogoutClicked() {
      const self = this;
      const app = self.$f7;
      const router = self.$f7router;

      router.navigate("/");      
    }
  },
};
</script>



