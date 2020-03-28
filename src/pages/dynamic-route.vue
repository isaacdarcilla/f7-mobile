<template>
  <f7-page @page:beforeremove="onPageBeforeRemove" @page:beforeout="onPageBeforeOut">
    <form v-on:submit.prevent="" action="" method="POST">
    <f7-navbar v-for="(value, key) in $f7route.query" :key="key" :title="value" back-link="Back">
      <f7-nav-right>
        <f7-link
          sheet-open=".corrective"
          icon-ios="f7:add"
          icon-aurora="f7:add"
          icon-md="material:add"
        ></f7-link>
      </f7-nav-right>    
    </f7-navbar>
    <f7-block-title>Desktop Preview</f7-block-title>
    <f7-block>
      <p>
        You can update the values of the desktop as long as it is a Preventive Maintenance update. Note that all values are required to fill in.
      </p>      
    </f7-block>
      <f7-sheet class="corrective" style="height:auto" swipe-to-close backdrop>
        <div class="swipe-handler"></div>
        <form v-on:submit.prevent="AddActions" action="" method="GET">
        <f7-page-content>
            <f7-block-title medium>Corrective Action</f7-block-title>
            <f7-list no-hairlines-md>
              <f7-list-input
                label="Corrective Action"
                type="text"
                :value="correctiveaction"
                @input="correctiveaction = $event.target.value"
                placeholder="Type the corrective action "
                required
                validate
                clear-button
              >
              </f7-list-input>
              <f7-list-input
                label="Responsible"
                type="text"
                :value="responsible"
                @input="responsible = $event.target.value"
                placeholder="Type who is responsible"
                required
                validate
                clear-button
              >
              </f7-list-input>      
              <f7-list-input
                label="Remarks"
                type="text"
                :value="correctiveremarks"
                @input="correctiveremarks = $event.target.value"
                placeholder="Type corrective remarks"
                required
                validate
                clear-button
              >
              </f7-list-input>                         
            </f7-list>
            <f7-block>
              <f7-button type="submit" fill>Add</f7-button>
            </f7-block>
          </f7-page-content>
        </form>
      </f7-sheet>    
    <f7-list media-list>
      <f7-list-item v-for="desktop in desktops"
        sheet-open=".desktopname"
        :link="desktop.link"
        :title="desktop.desktopname"
        after="Edit"
        text="Desktop Name"
      >
      <f7-sheet class="desktopname" style="height:auto" swipe-to-close backdrop>
        <div class="swipe-handler"></div>
        <form v-on:submit.prevent="UpdateDesktopName" action="" method="GET">
        <f7-page-content>
            <f7-block-title medium>Update Name</f7-block-title>
            <f7-list no-hairlines-md>
              <f7-list-input
                label="Desktop Name"
                type="text"
                :value="desktopname"
                @input="desktopname = $event.target.value"
                placeholder="Type the new desktop name "
                required
                validate
                clear-button
              >
              </f7-list-input>
            </f7-list>
            <f7-block>
              <f7-button type="submit" fill>Update Name</f7-button>
            </f7-block>
          </f7-page-content>
        </form>
      </f7-sheet>   
      </f7-list-item>
      <f7-list-item v-for="desktop in desktops"
        sheet-open=".location"
        :link="desktop.link"
        :title="desktop.location"
        after="Edit"
        text="Desktop Location"
      >
      <f7-sheet class="location" style="height:auto" swipe-to-close backdrop>
        <div class="swipe-handler"></div>
        <form v-on:submit.prevent="UpdateDesktopLocation" action="" method="GET">
        <f7-page-content>
            <f7-block-title medium>Update Location</f7-block-title>
            <f7-list no-hairlines-md>
              <f7-list-input
                label="Desktop Location"
                type="text"
                :value="location"
                @input="location = $event.target.value"
                placeholder="Type the new desktop location"
                required
                validate
                clear-button
              >
              </f7-list-input>
            </f7-list>
            <f7-block>
              <f7-button type="submit" fill>Update Location</f7-button>
            </f7-block>
          </f7-page-content>
        </form>
      </f7-sheet>           
      </f7-list-item>
      <f7-list-item v-for="desktop in desktops"
        sheet-open=".model"
        :link="desktop.link"
        :title="desktop.model"
        after="Edit"
        text="Desktop Model"
      >
      <f7-sheet class="model" style="height:auto" swipe-to-close backdrop>
        <div class="swipe-handler"></div>
        <form v-on:submit.prevent="UpdateDesktopModel" action="" method="GET">
        <f7-page-content>
            <f7-block-title medium>Update Model</f7-block-title>
            <f7-list no-hairlines-md>
              <f7-list-input
                label="Desktop Model"
                type="text"
                :value="model"
                @input="model = $event.target.value"
                placeholder="Type the new desktop model"
                required
                validate
                clear-button
              >
              </f7-list-input>
            </f7-list>
            <f7-block>
              <f7-button type="submit" fill>Update Model</f7-button>
            </f7-block>
          </f7-page-content>
        </form>
      </f7-sheet>        
      </f7-list-item>
      <f7-list-item v-for="desktop in desktops"
        sheet-open=".frequency"
        :link="desktop.link"
        :title="desktop.frequency"
        after="Edit"
        text="Frequency"
      >
      <f7-sheet class="frequency" style="height:auto" swipe-to-close backdrop>
        <div class="swipe-handler"></div>
        <form v-on:submit.prevent="UpdateDesktopFrequency" action="" method="GET">
        <f7-page-content>
            <f7-block-title medium>Update Frequency</f7-block-title>
            <f7-list no-hairlines-md>
              <f7-list-input
                label="Frequency"
                type="text"
                :value="frequency"
                @input="frequency = $event.target.value"
                placeholder="Type the new frequency"
                required
                validate
                clear-button
              >
              </f7-list-input>
            </f7-list>
            <f7-block>
              <f7-button type="submit" fill>Update Frequency</f7-button>
            </f7-block>
          </f7-page-content>
        </form>
      </f7-sheet>            
      </f7-list-item>
      <f7-list-item v-for="desktop in desktops"
        sheet-open=".updatedon"
        :link="desktop.link"
        :title="desktop.updatedon"
        after="Edit"
        text="Maintenance Date"
      >
      <f7-sheet class="updatedon" style="height:auto" swipe-to-close backdrop>
        <div class="swipe-handler"></div>
        <form v-on:submit.prevent="UpdateDesktopDate" action="" method="GET">
        <f7-page-content>
            <f7-block-title medium>Update Date</f7-block-title>
            <f7-list no-hairlines-md>
              <!-- <f7-list-input
                label="Maintenance Date"
                type="datepicker"
                :value="updatedon"
                @input="(updatedon) => calendar.setValue(updatedon)"
                placeholder="Select new maintenance date"
                :calendar-params="{dateFormat: 'MM dd, yyyy'}"
                required
                validate
                clear-button
              >
              </f7-list-input> -->
            </f7-list>
            <f7-block>
              <f7-button type="submit" fill>Update Date</f7-button>
            </f7-block>
          </f7-page-content>
        </form>
      </f7-sheet>         
      </f7-list-item>
    </f7-list> 
    <f7-block-title>Checklist</f7-block-title>
    <f7-block>
      <p>
        You can select from the checklist status. Note that all values are required to fill in.
      </p>      
    </f7-block> 
    <f7-list media-list>
      <f7-list-item v-for="desktop in desktops"
        actions-open=".systemunit"
        link
        title="System Unit"
        :subtitle="desktop.rsystemunit"
        :after="desktop.systemunit"
        text="Check on/off button"
      >    
        <f7-actions class="systemunit">
          <f7-actions-group>
            <f7-actions-label><b>System Unit Status <span style="color: green">{{ desktop.systemunit }}</span></b></f7-actions-label>                    
            <f7-actions-button v-on:click="RemarksSystemUnit">Add Remarks</f7-actions-button>
            <f7-actions-button v-on:click="CheckSystemUnitOk">Status is okay</f7-actions-button>
            <f7-actions-button v-on:click="CheckSystemUnitNotOk">Status is not okay</f7-actions-button>
            <f7-actions-button color="red">Close</f7-actions-button>
          </f7-actions-group>
        </f7-actions> 
                      
      </f7-list-item>  
      <f7-list-item v-for="desktop in desktops"
        actions-open=".monitor"
        link
        title="Monitor"
        :subtitle="desktop.rmonitor"
        :after="desktop.monitor"
        text="Check monitor display"
      >
        <f7-actions class="monitor">
          <f7-actions-group>
            <f7-actions-label><b>Monitor Status <span style="color: green">{{ desktop.monitor }}</span></b></f7-actions-label>
            <f7-actions-button v-on:click="RemarksMonitor">Add Remarks</f7-actions-button>
            <f7-actions-button v-on:click="CheckMonitorOk">Status is okay</f7-actions-button>
            <f7-actions-button v-on:click="CheckMonitorNotOk">Status is not okay</f7-actions-button>
            <f7-actions-button color="red">Close</f7-actions-button>
          </f7-actions-group>
        </f7-actions>        
      </f7-list-item>   
      <f7-list-item v-for="desktop in desktops"
        actions-open=".keyboard"
        link
        title="Keyboard"
        :subtitle="desktop.rkeyboard"
        :after="desktop.keyboard"
        text="Check for sticky keys"
      >
        <f7-actions class="keyboard">
          <f7-actions-group>
            <f7-actions-label><b>Keyboard Status <span style="color: green">{{ desktop.keyboard }}</span></b></f7-actions-label>
            <f7-actions-button v-on:click="RemarksKeyboard">Add Remarks</f7-actions-button>
            <f7-actions-button v-on:click="CheckKeyboardOk">Status is okay</f7-actions-button>
            <f7-actions-button v-on:click="CheckKeyboardNotOk">Status is not okay</f7-actions-button>
            <f7-actions-button color="red">Close</f7-actions-button>
          </f7-actions-group>
        </f7-actions>        
      </f7-list-item>  
      <f7-list-item v-for="desktop in desktops"
        actions-open=".mouse"
        link
        title="Mouse"
        :subtitle="desktop.rmouse"
        :after="desktop.mouse"
        text="Check for mouse left/right buttons"
      >
        <f7-actions class="mouse">
          <f7-actions-group>
            <f7-actions-label bold><b>Mouse Status <span style="color: green">{{ desktop.mouse }}</span></b></f7-actions-label>
            <f7-actions-button v-on:click="RemarksMouse">Add Remarks</f7-actions-button>
            <f7-actions-button v-on:click="CheckMouseOk">Status is okay</f7-actions-button>
            <f7-actions-button v-on:click="CheckMouseNotOk">Status is not okay</f7-actions-button>
            <f7-actions-button color="red">Close</f7-actions-button>
          </f7-actions-group>
        </f7-actions>         
      </f7-list-item>  
      <f7-list-item v-for="desktop in desktops"
        actions-open=".avr"
        link
        title="AVR/UPS"
        :subtitle="desktop.ravr"
        :after="desktop.avr"
        text="Check on/off button"
      >
        <f7-actions class="avr">
          <f7-actions-group>
            <f7-actions-label bold><b>Power Supply Status <span style="color: green">{{ desktop.avr }}</span></b></f7-actions-label>
            <f7-actions-button v-on:click="RemarksAvr">Add Remarks</f7-actions-button>
            <f7-actions-button v-on:click="CheckAvrOk">Status is okay</f7-actions-button>
            <f7-actions-button v-on:click="CheckAvrNotOk">Status is not okay</f7-actions-button>
            <f7-actions-button color="red">Close</f7-actions-button>
          </f7-actions-group>
        </f7-actions>         
      </f7-list-item>  
      <f7-list-item v-for="desktop in desktops"
        actions-open=".printer"
        link
        title="Printer"
        :subtitle="desktop.rprinter"
        :after="desktop.printer"
        text="Check for printer"
      >
        <f7-actions class="printer">
          <f7-actions-group>
            <f7-actions-label><b>Printer Status <span style="color: green">{{ desktop.printer }}</span></b></f7-actions-label>
            <f7-actions-button v-on:click="RemarksPrinter">Add Remarks</f7-actions-button>
            <f7-actions-button v-on:click="CheckPrinterOk">Status is okay</f7-actions-button>
            <f7-actions-button v-on:click="CheckPrinterNotOk">Status is not okay</f7-actions-button>
            <f7-actions-button color="red">Close</f7-actions-button>
          </f7-actions-group>
        </f7-actions>         
      </f7-list-item>  
      <f7-list-item v-for="desktop in desktops"
        actions-open=".software"
        link
        title="Software"
        :subtitle="desktop.rsoftware"
        :after="desktop.software"
        text="Update antivirus and system scan"
      >
        <f7-actions class="software">
          <f7-actions-group>
            <f7-actions-label><b>Software Status <span style="color: green">{{ desktop.software }}</span></b></f7-actions-label>
            <f7-actions-button v-on:click="RemarksSoftware">Add Remarks</f7-actions-button>
            <f7-actions-button v-on:click="CheckSoftwareOk">Status is okay</f7-actions-button>
            <f7-actions-button v-on:click="CheckSoftwareNotOk">Status is not okay</f7-actions-button>
            <f7-actions-button color="red">Close</f7-actions-button>
          </f7-actions-group>
        </f7-actions>         
      </f7-list-item>   
      <f7-list-item v-for="desktop in desktops"
        actions-open=".others"
        link
        title="Others"
        :subtitle="desktop.rothers"
        :after="desktop.others"
        text="Other checklist"
      >
        <f7-actions class="others">
          <f7-actions-group>
            <f7-actions-label><b>Others Status <span style="color: green">{{ desktop.others }}</span></b></f7-actions-label>
            <f7-actions-button v-on:click="RemarksOthers">Add Remarks</f7-actions-button>
            <f7-actions-button v-on:click="CheckOthersOk">Status is okay</f7-actions-button>
            <f7-actions-button v-on:click="CheckOthersNotOk">Status is not okay</f7-actions-button>
            <f7-actions-button color="red">Close</f7-actions-button>
          </f7-actions-group>
        </f7-actions>         
      </f7-list-item>                                              
    </f7-list>

    <f7-block-title>Corrective Actions</f7-block-title>
    <f7-block>
      <p>
        Corrective actions are added when desktop is condemned or follow up actions are required.
      </p>      
    </f7-block>
    <f7-list media-list>
      <f7-list-item v-for="action in actions"
        swipeout
        :title="action.action"
        :after="action.responsible"
        :text="action.remarks"
        :subtitle="action.due"
      >
        <f7-swipeout-actions right>  
          <f7-swipeout-button color="orange" delete v-on:click="DeleteActions(action.id)">Delete</f7-swipeout-button>      
        </f7-swipeout-actions>       
      </f7-list-item>
    </f7-list>

<!--     <f7-block-title>Checked By</f7-block-title>
    <f7-block>
      <p>
        Desktop unit preventive maintenance checked and approved by.
      </p>      
    </f7-block>   -->  
    <f7-block strong>
      <f7-link @click="$f7router.navigate('/home')">Go back to Dashboard</f7-link>
    </f7-block>
  </form>
  </f7-page>
</template>
<script>
import {
  f7Page,
  f7Navbar,
  f7NavLeft,
  f7NavTitle,
  f7NavTitleLarge,
  f7NavRight,
  f7BlockTitle,
  f7List,
  f7ListItem,
  f7Link,
  f7Searchbar,
  f7Icon,
  f7Sheet,
  f7Actions,
  f7ActionsGroup,
  f7ActionsLabel,
  f7ActionsButton
} from "framework7-vue";

import $ from "jquery";
import axios from "axios";

export default {
  data() {
    return {
      desktops: [],
      desktop: "",
      desktopname: "",
      location: "",
      model: "",
      updatedon: "",
      frequency: "",
      remarks: "",
      correctiveaction: "",
      correctiveremarks: "",
      responsible: "",
      actions: [],
      action: "",
    }
  },

  methods: {
    FetchDekstopsByName: function(){
      var self = this
      var desktopName = this.$f7route.query.desktopname
      var api = "https://querybackend.herokuapp.com/fetch-desktops-by-name.php?desktopname=" + desktopName;
      console.log(desktopName);
      console.log(api);
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.desktops = json;
        }
      })
    },
    FetchActions: function(){
      var self = this
      var desktopName = this.$f7route.query.desktopname
      var api = "https://querybackend.herokuapp.com/fetch-actions.php?desktopname=" + desktopName;
      console.log(desktopName);
      console.log(api);
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.actions = json;
        }
      })
    },    
    UpdateDesktopName: function(){
      var self = this
      const router = self.$f7router;
      var desktopName = this.$f7route.query.desktopname;
      var desktopLink = "/dynamic/d/2016/?desktopname=" + this.desktopname;
      var api = "https://querybackend.herokuapp.com/update-desktop-by-name.php?desktopname=" + desktopName + "&name=" + this.desktopname + "&link=" + desktopLink;
      console.log(api)
      console.log(this.desktopname)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.desktopname = json;
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    UpdateDesktopLocation: function(){
      var self = this
      const router = self.$f7router;
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/update-desktop-by-location.php?desktopname=" + desktopName + "&location=" + this.location;
      console.log(api)
      console.log(this.location)  
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.location = json;
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    UpdateDesktopModel: function(){
      var self = this
      const router = self.$f7router;
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/update-desktop-by-model.php?desktopname=" + desktopName + "&model=" + this.model;
      console.log(api)
      console.log(this.model)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.model = json;
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    UpdateDesktopFrequency: function(){
      var self = this
      const router = self.$f7router;
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/update-desktop-by-frequency.php?desktopname=" + desktopName + "&frequency=" + this.frequency;
      console.log(api)
      console.log(this.frequency)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.frequency = json;
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },  
    UpdateDesktopDate: function(){
      var self = this
      const router = self.$f7router;
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/update-desktop-by-date.php?desktopname=" + desktopName + "&date=" + this.updatedon;
      console.log(api)
      console.log(self.updatedon)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.updatedon = json;
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckKeyboardOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-keyboard-unit.php?desktopname=" + desktopName + "&status=Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckKeyboardNotOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-keyboard-unit.php?desktopname=" + desktopName + "&status=Not Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckMouseOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-mouse-unit.php?desktopname=" + desktopName + "&status=Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckMouseNotOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-mouse-unit.php?desktopname=" + desktopName + "&status=Not Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },     
    CheckAvrOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-avr-unit.php?desktopname=" + desktopName + "&status=Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckAvrNotOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-avr-unit.php?desktopname=" + desktopName + "&status=Not Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },      
    CheckPrinterOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-printer-unit.php?desktopname=" + desktopName + "&status=Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckPrinterNotOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-printer-unit.php?desktopname=" + desktopName + "&status=Not Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },    
    CheckSoftwareOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-software-unit.php?desktopname=" + desktopName + "&status=Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckSoftwareNotOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-software-unit.php?desktopname=" + desktopName + "&status=Not Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    }, 
    CheckOthersOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-others-unit.php?desktopname=" + desktopName + "&status=Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckOthersNotOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-others-unit.php?desktopname=" + desktopName + "&status=Not Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },                          
    CheckMonitorOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-monitor-unit.php?desktopname=" + desktopName + "&status=Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckMonitorNotOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-monitor-unit.php?desktopname=" + desktopName + "&status=Not Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },        
    CheckSystemUnitOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-system-unit.php?desktopname=" + desktopName + "&status=Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },
    CheckSystemUnitNotOk: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      var api = "https://querybackend.herokuapp.com/check-system-unit.php?desktopname=" + desktopName + "&status=Not Checked"
      console.log(api)
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    }, 

    RemarksSystemUnit: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      const app = self.$f7;
        app.dialog.prompt('Type remarks in the textbox below', 'Remarks', (name) => {
          var api = "https://querybackend.herokuapp.com/remarks-system-unit.php?desktopname=" + desktopName + "&remarks=" +  `${name}`;
          console.log(api)
          $.ajax({
            url: api,
            type: "get",
            dataType: "json",
            async: true,
            success: function(json){
              self.FetchDekstopsByName()
            }
          })          
          this.openPreloader()
        });
    },   
    RemarksMonitor: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      const app = self.$f7;
        app.dialog.prompt('Type remarks in the textbox below', 'Remarks', (name) => {
          var api = "https://querybackend.herokuapp.com/remarks-monitor.php?desktopname=" + desktopName + "&remarks=" +  `${name}`;
          console.log(api)
          $.ajax({
            url: api,
            type: "get",
            dataType: "json",
            async: true,
            success: function(json){
              self.FetchDekstopsByName()
            }
          })          
          this.openPreloader()
        });
    },  
    RemarksOthers: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      const app = self.$f7;
        app.dialog.prompt('Type remarks in the textbox below', 'Remarks', (name) => {
          var api = "https://querybackend.herokuapp.com/remarks-others.php?desktopname=" + desktopName + "&remarks=" +  `${name}`;
          console.log(api)
          $.ajax({
            url: api,
            type: "get",
            dataType: "json",
            async: true,
            success: function(json){
              self.FetchDekstopsByName()
            }
          })          
          this.openPreloader()
        });
    },   
    RemarksPrinter: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      const app = self.$f7;
        app.dialog.prompt('Type remarks in the textbox below', 'Remarks', (name) => {
          var api = "https://querybackend.herokuapp.com/remarks-printer.php?desktopname=" + desktopName + "&remarks=" +  `${name}`;
          console.log(api)
          $.ajax({
            url: api,
            type: "get",
            dataType: "json",
            async: true,
            success: function(json){
              self.FetchDekstopsByName()
            }
          })          
          this.openPreloader()
        });
    },   
    RemarksAvr: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      const app = self.$f7;
        app.dialog.prompt('Type remarks in the textbox below', 'Remarks', (name) => {
          var api = "https://querybackend.herokuapp.com/remarks-avr.php?desktopname=" + desktopName + "&remarks=" +  `${name}`;
          console.log(api)
          $.ajax({
            url: api,
            type: "get",
            dataType: "json",
            async: true,
            success: function(json){
              self.FetchDekstopsByName()
            }
          })          
          this.openPreloader()
        });
    },     
    RemarksSoftware: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      const app = self.$f7;
        app.dialog.prompt('Type remarks in the textbox below', 'Remarks', (name) => {
          var api = "https://querybackend.herokuapp.com/remarks-software.php?desktopname=" + desktopName + "&remarks=" +  `${name}`;
          console.log(api)
          $.ajax({
            url: api,
            type: "get",
            dataType: "json",
            async: true,
            success: function(json){
              self.FetchDekstopsByName()
            }
          })          
          this.openPreloader()
        });
    },      
    RemarksMouse: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      const app = self.$f7;
        app.dialog.prompt('Type remarks in the textbox below', 'Remarks', (name) => {
          var api = "https://querybackend.herokuapp.com/remarks-mouse.php?desktopname=" + desktopName + "&remarks=" +  `${name}`;
          console.log(api)
          $.ajax({
            url: api,
            type: "get",
            dataType: "json",
            async: true,
            success: function(json){
              self.FetchDekstopsByName()
            }
          })          
          this.openPreloader()
        });
    }, 
    RemarksKeyboard: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      const app = self.$f7;
        app.dialog.prompt('Type remarks in the textbox below', 'Remarks', (name) => {
          var api = "https://querybackend.herokuapp.com/remarks-keyboard.php?desktopname=" + desktopName + "&remarks=" +  `${name}`;
          console.log(api)
          $.ajax({
            url: api,
            type: "get",
            dataType: "json",
            async: true,
            success: function(json){
              self.FetchDekstopsByName()
            }
          })          
          this.openPreloader()
        });
    },     
    AddActions: function(){
      var self = this
      const router = self.$f7router;
      var desktopName = this.$f7route.query.desktopname
      var api = "https://querybackend.herokuapp.com/corrective-actions.php?desktopname=" + desktopName + "&actions=" + this.correctiveaction + "&remarks=" + this.correctiveremarks + "&responsible=" + this.responsible
      console.log(api)  
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json){
          self.location = json;
          self.FetchDekstopsByName()
        }
      })
      this.openPreloader();
      this.onPageBeforeOut();
    },  
    DeleteActions: function(id) {
      var self = this;
      var api = "https://querybackend.herokuapp.com/delete-actions.php?desktopname=" + id;
      console.log(api)  
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json) { 
        }
      });  
    },      
    AddNoted: function(){
      var self = this
      const router = self.$f7router
      var desktopName = this.$f7route.query.desktopname;
      const app = self.$f7;
        app.dialog.prompt('Type your name in the textbox below', 'Checked', (name) => {
          var api = "https://querybackend.herokuapp.com/add-checker.php?desktopname=" + desktopName + "&remarks=" +  `${name}`;
          console.log(api)
          $.ajax({
            url: api,
            type: "get",
            dataType: "json",
            async: true,
            success: function(json){
              self.FetchDekstopsByName()
            }
          })          
          this.openPreloader()
        });
    },         
    openPreloader() {
      const app = this.$f7;
      app.dialog.preloader("Loading data...");
      setTimeout(() => {
        app.dialog.close();
        this.FetchDekstopsByName();
      }, 2000);
    },  
    onPageBeforeOut() {
      const self = this;
      self.$f7.sheet.close();
      this.FetchActions();
    },
    onPageBeforeRemove() {
      const self = this;
      if (self.sheet) self.sheet.destroy();
    },                           
  },  
  mounted() {
    const self = this;
    const app = self.$f7;
    const router = self.$f7router;

    this.openPreloader()
    this.FetchDekstopsByName()
    this.FetchActions()
  }
};
</script>
