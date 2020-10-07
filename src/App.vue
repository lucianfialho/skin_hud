<template>
	<div id="app" class="main" v-if="showSkinHud">
		<section class="left-tabs">
			<b-tabs v-model="activeTab">
				<template v-for="tab in components">
					<b-tab-item :key="tab.id" :label="tab.label" :value="tab.id" >
						<template v-for="property in tab.inputs">
							<b-field :key="property.id" :value="property.id" :label="property.name">
								<b-slider :min="property.min" :value="property.value" @change="changeCameraOffset(property.camOffset)" :max="property.max" ticks></b-slider>
							</b-field>
						</template>
					</b-tab-item>
				</template>
			</b-tabs>
		</section>
  	</div>
</template>

<script>
	const axios = require('axios').default;
	export default {
		name: 'app',
		components: {},
		data() {
			return {
				activeTab: 'body',
				showSkinHud: false,
				character: ['sex','face','skin','age_1','age_2','eye_color','beard_1','beard_2','beard_3','beard_4','hair_1','hair_2','hair_color_1','hair_color_2','eyebrows_1','eyebrows_2','eyebrows_3','eyebrows_4','makeup_1','makeup_2','makeup_3','makeup_4','lipstick_1','lipstick_2','lipstick_3','lipstick_4','blemishes_1','blemishes_2','blush_1','blush_2','blush_3','complexion_1','complexion_2','sun_1','sun_2','moles_1','moles_2','chest_1','chest_2','chest_3','bodyb_1','bodyb_2'],
				components: [
					{
						id: 'face',
						label: 'Feições',
						//inputs: [{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"sex","label":"Sex","max":1,"value":0},{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"face","label":"Face","max":45,"value":0}],
						inputs: [],
						camOffset: '0.65'
					},
					{
						id: 'body',
						label: 'Torso',
						// inputs: [{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"sex","label":"Sex","max":1,"value":0},{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"face","label":"Face","max":45,"value":0}],
						inputs: [],
						camOffset: '0.15'
					},
					{
						id: 'legs',
						label: 'Pernas',
						// inputs: [{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"sex","label":"Sex","max":1,"value":0},{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"face","label":"Face","max":45,"value":0}],
						inputs: [],
						camOffset: '-0.5'
					},
					{
						id: 'feets',
						label: 'Sapatos',
						// inputs: [{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"sex","label":"Sex","max":1,"value":0},{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"face","label":"Face","max":45,"value":0}],
						inputs: [],
						camOffset: '-0.8'
					},
					{
						id: 'accessories',
						label: 'Roupas e acessórios',
						// inputs: [{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"sex","label":"Sex","max":1,"value":0},{"camOffset":0.65,"min":0,"zoomOffset":0.6,"name":"face","label":"Face","max":45,"value":0}],
						inputs: [],
						camOffset: '0.75'
					}
				]
			}
		},
		destroyed() {
			window.removeEventListener('message', this.listener);
		},
		mounted() {
			this.listener = window.addEventListener(
				'message',
				event => {
					const item = event.data;
					
					if(item.showSkinHud === true) this.showSkinHud = true 
					
					if(item.components) {
						//  -0.8 = Feets
						//  -0.5 = Legs
						//  0.65 = Face
						//  0.15 = Body

						this.components.map((component) => {
							if(component.id == 'feets') component.inputs = item.components.filter((element) => (element.camOffset == -0.8))
							if(component.id == 'legs') component.inputs = item.components.filter((element) => (element.camOffset == -0.5 ))
							if(component.id == 'face') component.inputs = item.components.filter((element) => (element.camOffset == 0.65 && this.character.includes(element.name)))
							if(component.id == 'body') component.inputs = item.components.filter((element) => (element.camOffset == 0.15 ))
							if(component.id == 'accessories') component.inputs = item.components.filter((element) => (!this.character.includes(element.name)))
							
						})
					}
				},
				false,
			);
		},
		methods: {
			sendData (name, data) {
				axios.post(`http://esx_skin_hud/${name}`, {data: data})
			},
			changeCameraOffset (camOffset) {
				this.sendData('esx_skin_hud:ChangeCamera', camOffset)
			},
			
		}
	};
</script>

<style lang="scss">
/* Want nice animations? Check out https://github.com/asika32764/vue2-animate */
/* @import 'https://unpkg.com/vue2-animate/dist/vue2-animate.min.css'; */
html {
	background: transparent;
    overflow-y: hidden;
    width: 30%;
}

.main {
  display: flex;
  flex-direction: row;
}

.left-tabs {
  width: 100%;
  background: #fff;
  height: 100%;
}
</style>
