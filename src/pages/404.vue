<template>
  <f7-page v-on:click="loadMore" name="home">
    <!-- Top Navbar -->
    <f7-navbar title="Archives" back-link="Back">   	
    </f7-navbar> 
    <!-- Page content-->
    <f7-block-title class="searchbar-found">Archived Desktops</f7-block-title>
     <f7-block>
      <p>
        You can view archived desktops here. Swipeout the desktop to show more options. You can either unarchive or completely remove the desktop.
      </p>      
    </f7-block>
    <f7-list media-list class="components-list searchbar-found">
      <f7-list-item
        swipeout
        @swipeout:deleted
        v-for="desktop in desktops"
        :title="desktop.desktopname"
        after="Swipe"
        :subtitle="desktop.location"
        :text="desktop.updatedon"
      >
        <f7-swipeout-actions right>
          <f7-swipeout-button color="orange" delete v-on:click="Delete(desktop.desktopname)">Delete Archive</f7-swipeout-button>
        </f7-swipeout-actions> 
        <f7-swipeout-actions left>
          <f7-swipeout-button color="green" v-on:click="MoveToDashboard(desktop.desktopname)">Unarchive</f7-swipeout-button>
        </f7-swipeout-actions>                  
      </f7-list-item>
    </f7-list>
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
  f7Icon
} from "framework7-vue";

import $ from "jquery";

export default {
  data() {
    return {
      desktops: [],
      desktop: ""
    };
  },

  methods: {
    FetchDekstops: function() {
      var self = this;
      var api = "https://querybackend.herokuapp.com/fetch-desktop-archives.php";
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json) {
          self.desktops = json;
        }
      });
    },
    loadMore: function() {
        this.FetchDekstops()
    },
    openPreloader() {
      const app = this.$f7;
      app.dialog.preloader("Loading data...");
      setTimeout(() => {
        app.dialog.close();
        this.FetchDekstops()
      }, 3000);
    },    
    onDeleted() {
      const app = this.$f7;
      app.dialog.alert("Desktop has been moved back to dashboard.", "Desktop Unarchive");
    },
    onDelete() {
      const app = this.$f7;
      app.dialog.alert("Desktop has been removed.", "Desktop Removed");
    },    
    MoveToDashboard: function(desktopname){
      var self = this;
      var api = "https://querybackend.herokuapp.com/unarchive-desktops.php?desktopname=" + desktopname;
      this.onDeleted()
      this.FetchDekstops()
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json) {
          console.log(desktopname)
          console.log(api)   
        }
      });         
    },
    Delete: function(desktopname){
      var self = this;
      var api = "https://querybackend.herokuapp.com/unarchive-delete-desktops.php?desktopname=" + desktopname;
      this.onDelete();
      $.ajax({
        url: api,
        type: "get",
        dataType: "json",
        async: true,
        success: function(json) {
          console.log(desktopname)
          console.log(api)   
          this.FetchDekstops()
        }
      });         
    },       
  },
  mounted() {
    this.openPreloader();
    this.FetchDekstops();
  }
};
</script>
