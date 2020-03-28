<template>
	<f7-app :params="f7params">
		<!-- Status bar overlay for fullscreen mode-->
		<f7-statusbar></f7-statusbar>
		<!-- Left panel with cover effect-->
		<!--   <f7-panel left cover theme-dark>
<f7-view>
<f7-page>
<f7-navbar title="Dashboard"></f7-navbar>
<f7-block>Left panel content goes here</f7-block>
</f7-page>
</f7-view>
</f7-panel> -->
		<!-- Views/Tabs container -->
		<f7-views tabs class="safe-areas" themeDark>
			<!-- Tabbar for switching views-tabs -->
			<f7-toolbar themeDark tabbar labels bottom>
				<f7-link tab-link="#view-home" tab-link-active>
					<f7-icon
						ios="f7:home_fill"
						aurora="f7:home_fill"
						md="material:home"
					>
						<f7-badge color="green" v-for="count in counts">{{ count.counts }}</f7-badge>
					</f7-icon>
					<span class="tabbar-label">Dashboard</span>
				</f7-link>
				<f7-link tab-link="#view-catalog">
					<f7-icon
						ios="f7:flag_fill"
						aurora="f7:flag_fill"
						md="material:flag"
					>
						<f7-badge color="red" v-for="archive in archives">{{ archive.archived }}</f7-badge>
					</f7-icon>
					<span class="tabbar-label">Unit Archive</span>
				</f7-link>
				<f7-link tab-link="#view-settings">
					<f7-icon
						ios="f7:person"
						aurora="f7:person"
						md="material:person"
					>
					</f7-icon>
					<span class="tabbar-label">Account</span>
				</f7-link>
			</f7-toolbar>
			<!-- Your main view/tab, should have "view-main" class. It also has "tab-active" class -->
			<f7-view id="view-home" main tab tab-active url="/"></f7-view>
			<!-- Catalog View -->
			<f7-view
				id="view-catalog"
				name="catalog"
				tab
				url="/catalog/"
			></f7-view>
			<!-- Settings View -->
			<f7-view
				id="view-settings"
				name="settings"
				tab
				url="/settings/"
			></f7-view>
		</f7-views>
	</f7-app>
</template>
<script>
import routes from "../js/routes.js";
import $ from "jquery";
export default {
	data() {
		return {
			f7params: {
				name: "f7-auth", // App name
				theme: "auto", // Automatic theme detection
				// App root data
				data: function() {
					return {
						user: {
							firstName: "John",
							lastName: "Doe"
						}
					};
				},
				// App routes
				routes: routes
			},
			// Login screen data
			username: "",
			password: "",
			counts: [],
			count: "",
			archives: [],
			archive: "",
		};
	},
	methods: {
		alertLoginData() {
			this.$f7.dialog.alert(
				"Username: " + this.username + "<br>Password: " + this.password
			);
		},
		CountDesktops: function() {
			var self = this;
			var api = "https://querybackend.herokuapp.com/count-desktops.php";
			$.ajax({
				url: api,
				type: "get",
				dataType: "json",
				async: true,
				success: function(json) {
					self.counts = json;
				}
			});
		},
		CountArchived: function() {
			var self = this;
			var api = "https://querybackend.herokuapp.com/count-archives.php";
			$.ajax({
				url: api,
				type: "get",
				dataType: "json",
				async: true,
				success: function(json) {
					self.archives = json;
				}
			});
		}		
	},
	mounted() {
		this.$f7ready(f7 => {
			// Call F7 APIs here
		});
		this.CountDesktops()
		this.CountArchived()
	}
};
</script>
