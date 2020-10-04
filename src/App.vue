<template>
  <div id="app" class="main">
	<section class="left-tabs">
	  <b-tabs v-model="activeTab">
		<b-tab-item v-for="tab in leftTabs" v-bind:key="tab.id" :label="tab.name">
		  <b-field v-for="property in tab.properties" v-bind:key="property.id" :label="property.name">
			<b-slider :min="property.min" :value="property.value" :max="property.max" ticks></b-slider>
		  </b-field>
		</b-tab-item>
	  </b-tabs>
	</section>
	<section class="character">0</section>
	<section class="right-tabs">
	  <b-tabs v-model="activeTab">
		<b-tab-item v-for="tab in rightTabs" v-bind:key="tab.id" :label="tab.name">
		  <b-field v-for="property in tab.properties" v-bind:key="property.id" :label="property.name">
			<b-slider :min="property.min" :value="property.value" :max="property.max" ticks></b-slider>
		  </b-field>
		</b-tab-item>
	  </b-tabs>
	</section>
  </div>
</template>

<script>
	import HelloWorld from './components/HelloWorld';
	import Nui from './utils/Nui';

	export default {
		name: 'app',
		components: {HelloWorld},
		data() {
		return {
			
		};
	},
		destroyed() {
		window.removeEventListener('message', this.listener);
		},
		mounted() {
		this.listener = window.addEventListener(
			'message',
			event => {
			const item = event.data || event.detail;
			if (this[item.type]) {
				this[item.type](item);
			}
			},
			false,
		);
		},
		methods: {},
	};
</script>

<style lang="scss">
/* Want nice animations? Check out https://github.com/asika32764/vue2-animate */
/* @import 'https://unpkg.com/vue2-animate/dist/vue2-animate.min.css'; */
.main {
  display: flex;
  flex-direction: row;
}

.left-tabs,
.character,
.right-tabs {
  width: 30%;
}
</style>
