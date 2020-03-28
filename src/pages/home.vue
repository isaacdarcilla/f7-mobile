<template>
  <f7-page v-on:click="loadMore" name="home">
    <!-- Top Navbar -->
    <f7-navbar title="Dashboard">
      <f7-nav-right>
        <f7-link
          class="searchbar-enable"
          data-searchbar=".searchbar-components"
          icon-ios="f7:search"
          icon-aurora="f7:search"
          icon-md="material:search"
        ></f7-link>
      </f7-nav-right>
      <f7-searchbar
        class="searchbar-components"
        search-container=".components-list"
        search-in="a"
        expandable
        :disable-button="!this.$theme.aurora"
      ></f7-searchbar>
    </f7-navbar> 
    <!-- Page content-->
    <f7-block-title class="searchbar-found">Query Dashboard</f7-block-title>
     <f7-block class="searchbar-hide-on-search">
      <p>
        You can view desktops in dashboard. Swipeout the desktop to show more options.
      </p>      
    </f7-block>    
    <f7-list media-list class="components-list searchbar-found">
      <f7-list-item
        swipeout
        @swipeout:deleted="onDeleted"
        v-for="desktop in desktops"
        :link="desktop.link"
        :title="desktop.desktopname"
        after="Details"
        :subtitle="desktop.location"
        :text="desktop.updatedon"
      >
        <f7-swipeout-actions right>
          <!-- <f7-swipeout-button color="green">Printout</f7-swipeout-button> -->    
          <f7-swipeout-button color="orange" delete v-on:click="MoveToArchive(desktop.desktopname)">Archive</f7-swipeout-button>      
        </f7-swipeout-actions>        
      </f7-list-item>
    </f7-list>
    <f7-list class="searchbar-not-found">
      <f7-list-item title="Nothing found"></f7-list-item>
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
      desktop: "",
      counts: [],
      count: "",
    };
  },

  methods: {
    FetchDekstops: function() {
      var self = this;
      var api = "https://querybackend.herokuapp.com/fetch-desktops.php";
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
      app.dialog.alert("Desktop has been moved to archives.", "Desktop Archive");
    },
    MoveToArchive: function(desktopname){
      var self = this;
      var api = "https://querybackend.herokuapp.com/archive-desktops.php?desktopname=" + desktopname;
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
    Reload: function() {
      var self = this
      const router = self.$f7router
      router.navigate("/home");      
    }, 
  },
  mounted() {
    this.openPreloader();
    this.FetchDekstops();
  }
};
</script>
