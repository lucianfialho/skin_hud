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
			leftActiveTab: 1,
			rightActiveTab: 1,

			leftTabs: [
				{
					name: 'Parents', // Pais
					properties: [
					{
						name: 'Father Face', // Rosto do pai
						value: 0,
						min: 0,
						max: 45,
					},
					{
						name: 'Father ancestry', // Ascendência do pai
						value: 0,
						min: 0,
						max: 45,
					},
					{
						name: 'Mother Face', // Rosto da mãe
						value: 0,
						min: 0,
						max: 45,
					},
					{
						name: 'Mother ancestry', // Ascendência da mãe
						value: 0,
						min: 0,
						max: 45,
					},
					{
						name: 'Face dominant gene', // Rosto gene dominante
						value: 0,
						min: -100,
						max: 100,
					},
					{
						name: 'Ancestry dominant gene', // Gene ancestral dominante
						value: 0,
						min: -100,
						max: 100,
					},
					],
				},
				{
					name: 'Eyes', // Olhos
					properties: [
					{
						name: 'Eye state', // Estado dos olhos
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Eye color', // Cor dos olhos
						value: 0,
						min: 0,
						max: 31,
					},
					{
						name: 'Eyebrows', // Sobrancelhas
						value: 0,
						min: 0,
						max: 33,
					},
					{
						name: 'Eyebrow color', // Cor da sobrancelha
						value: 0,
						min: 0,
						max: 64,
					},
					{
						name: 'Brow width', // Largura da sobrancelha
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Brow shape', // Formato da sobrancelha
						value: 0,
						min: -1,
						max: 1,
					},
					],
				},
				{
					name: 'Nose', // Nariz
					properties: [
					{
						name: 'Nose Width', // Largura do nariz
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Nose height', // Altura do nariz
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Nose length', // Comprimento do nariz
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Nose bridge shift', // Mudança da ponte do nariz
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Nose tip', // Ponta do nariz
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Nose shift', // Mudança de nariz
						value: 0,
						min: -1,
						max: 1,
					},
					],
				},
				{
					name: 'Chin', // Queixo
					properties: [
					{
						name: 'Chin length', // Comprimento do queixo
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Chin position', // Posição do queixo
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Chin width', // Largura do queixo
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Chin height', // Altura do queixo
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Jaw width', // Largura da mandíbula
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Jaw height', // Altura da mandíbula
						value: 0,
						min: -1,
						max: 1,
					},
					],
				},
				{
					name: 'Cheek', // Bochecha
					properties: [
					{
						name: 'Cheekbone height', // Altura da bochecha
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Cheekbone width', // Largura da bochecha
						value: 0,
						min: -1,
						max: 1,
					},
					{
						name: 'Cheeks width', // Largura das bochechas
						value: 0,
						min: -1,
						max: 1,
					},
					],
				},
				{
					name: 'Lips', // Lábios
					properties: [
					{
						name: 'Lips width', // Largura dos lábios
						value: 0,
						min: -1,
						max: 1,
					},
					],
				},
				{
					name: 'Neck', // Altura do pescoço
					properties: [
					{
						name: 'Neck height', // Altura do pescoço
						value: 0,
						min: -1,
						max: 1,
					},
					],
				},
			],

			rightTabs: [
				{
					name: 'Face', // Rosto
					properties: [
					{
						name: 'Blemishes', // Manchas
						value: 0,
						min: 0,
						max: 24,
					},
					{
						name: 'Freckles', // Sardas
						value: 0,
						min: 0,
						max: 18,
					},
					{
						name: 'Complexion', // Aspecto
						value: 0,
						min: 0,
						max: 12,
					},
					{
						name: 'Blush', // Blush
						value: 0,
						min: 0,
						max: 7,
					},
					{
						name: 'Blush color', // Cor do Blush
						value: 0,
						min: 0,
						max: 63,
					},
					],
				},
				{
					name: 'Hair', // Cabelo
					properties: [
						{
							name: 'Hair', // Cabelo
							value: 0,
							min: 0,
							max: 37,
						},
						{
							name: 'Hair color', // Cor do Cabelo
							value: 0,
							min: 0,
							max: 63,
						},
						{
							name: 'Hair highlight', // Cor do Secundária do Cabelo
							value: 0,
							min: 0,
							max: 63,
						},
					]
				},
				{
					name: 'Beard', // Barba
					properties: [
						{
							name: 'Beard', // Barba
							value: 0,
							min: 0,
							max: 28,
						},
						{
							name: 'Beard color', // Cor da Barba
							value: 0,
							min: 0,
							max: 63,
						}
					]
				},
				{
					name: 'Makeup', // Maquiagem
					properties: [
						{
							name: 'Makeup', // Maquiagem
							value: 0,
							min: 0,
							max: 71,
						},
						{
							name: 'Lipstick', // Batom
							value: 0,
							min: 0,
							max: 9,
						},
						{
							name: 'Lipstick color', // Cor do Batom
							value: 0,
							min: 0,
							max: 63,
						}
					]
				},
				{
					name: 'Ageing', // Envelhecimento
					properties: [
						{
							name: 'Ageing', // Envelhecimento
							value: 0,
							min: 0,
							max: 14,
						}
					]
				},
				{
					name: 'Chest', // Pelo Corporal
					properties: [
						{
							name: 'Chest hair', // Pelo Corporal
							value: 0,
							min: 0,
							max: 16,
						},
						{
							name: 'Chest hair color', // Cor do Pelo Corporal
							value: 0,
							min: 0,
							max: 63,
						}
					]
				},
				{
					name: 'Body', // Corpo
					properties: [
						{
							name: 'Sun damage', // Dano Solar
							value: 0,
							min: 0,
							max: 11,
						},
						{
							name: 'Body blemishes', // Manchas no Corpo
							value: 0,
							min: 0,
							max: 12,
						},
						{
							name: 'More body blemishes', // Mais manchas corporais
							value: 0,
							min: 0,
							max: 1,
						}
					]
				},
			],
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
