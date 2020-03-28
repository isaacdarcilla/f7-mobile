<template>
  <f7-page name="home">
    <!-- Top Navbar -->
    <form v-on:submit.prevent="onCreate" action="" method="GET">
      <f7-navbar title="New Desktop">
        <f7-nav-right class="create">
          <f7-button type="submit"><b>Add</b></f7-button>
        </f7-nav-right>
      </f7-navbar>
      <f7-block-title>Add New Desktop</f7-block-title>
      <f7-block>
        <p>
          You can add new desktop here. Every desktop name must be unique and cannot be duplicated. Note that all values are required to fill in.
        </p>      
      </f7-block>      
      <f7-list class="login-list">
        <f7-list-input
          label="Desktop Name"
          type="text"
          placeholder="Desktop Name"
          :value="desktopname"
          @input="desktopname = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>
        <f7-list-input
          label="Location"
          type="text"
          placeholder="Location of Desktop"
          :value="location"
          @input="location = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>
        <f7-list-input
          label="Type/Model"
          type="text"
          placeholder="Model of Desktop"
          :value="model"
          @input="model = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>
        <f7-list-input
          label="Operating System"
          type="text"
          placeholder="Operating System"
          :value="os"
          @input="os = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>   
        <f7-list-input
          label="Monitor"
          type="text"
          placeholder="Monitor Model"
          :value="monitor"
          @input="monitor = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input> 
        <f7-list-input
          label="Motherboard"
          type="text"
          placeholder="Motherboard Model"
          :value="motherboard"
          @input="motherboard = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input> 
        <f7-list-input
          label="Memory"
          type="text"
          placeholder="Memory Size"
          :value="memory"
          @input="memory = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>    
        <f7-list-input
          label="Hard Disk"
          type="text"
          placeholder="Hard Disk Size"
          :value="disk"
          @input="disk = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>  
        <f7-list-input
          label="DVD Drive"
          type="text"
          placeholder="DVD Drive Model"
          :value="dvd"
          @input="dvd = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input> 
        <f7-list-input
          label="Mouse"
          type="text"
          placeholder="Mouse Model"
          :value="mouse"
          @input="mouse = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>    
        <f7-list-input
          label="Keyboard"
          type="text"
          placeholder="Keyboard Model"
          :value="keyboard"
          @input="keyboard = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>  
        <f7-list-input
          label="Printer"
          type="text"
          placeholder="Printer Model"
          :value="printer"
          @input="printer = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>
        <f7-list-input
          label="UPS"
          type="text"
          placeholder="UPS Model"
          :value="ups"
          @input="ups = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>
        <f7-list-input
          label="AVR"
          type="text"
          placeholder="AVR Model"
          :value="avr"
          @input="avr = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>
        <f7-list-input
          label="Remarks"
          type="text"
          placeholder="Desktop Remarks"
          :value="remarks"
          @input="remarks = $event.target.value"
          required
          validate
          clear-button
        ></f7-list-input>
      </f7-list>
    </form>
    <f7-block strong>
      <f7-link @click="$f7router.navigate('*')">Go to Archives</f7-link>
    </f7-block>    
  </f7-page>
</template>

<script>

import $ from "jquery";

export default {
  data() {
    return {
      desktopname: "",
      location: "",
      model: "",
      os: "",
      monitor: "",
      motherboard: "",
      memory: "",
      disk: "",
      dvd: "",
      mouse: "",
      keyboard: "",
      printer: "",
      ups: "",
      avr: "",
      remarks: "",
      counts: [],
      count: "",
    };
  },

  methods: {
    onCreate: function(){
      var self = this
      const router = self.$f7router;
      var api = "https://querybackend.herokuapp.com/create-new-desktop.php?desktopname=" + this.desktopname + "&location=" + this.location + "&model=" + this.model + "&os=" + this.os +
        "&monitor=" + this.monitor + "&motherboard=" + this.motherboard + "&memory=" + this.memory + "&disk=" + this.disk + "&dvd=" + this.dvd + "&mouse=" + this.mouse +
        "&keyboard=" + this.keyboard + "&printer=" + this.printer + "&ups=" + this.ups + "&avr=" + this.avr + "&remarks=" + this.remarks 
      console.log(api)
      self.openPreloader()
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.location = json;
          self.FetchDesktops()
        }
      })     
    },
    CountDesktops: function() {
      var self = this
      var api = "https://querybackend.herokuapp.com/count-desktops"
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json) {
          self.counts = json
          this.FetchDekstops()
        }
      });
    },    
    openPreloader() {
      const app = this.$f7;
      app.dialog.preloader("Adding desktop...");
      setTimeout(() => {
        app.dialog.close();
        this.openAlert();
      }, 2000);
    }, 
    openAlert() {
      const app = this.$f7;
      app.dialog.alert("New desktop unit added.", "Success");
    },       
  },  
  mounted() {}
};
</script>
