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
    <section class="character">
      0
    </section>
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
  components: {
    HelloWorld,
  },
  data() {
    return {
      leftActiveTab: 1,
      rightActiveTab: 1,
      leftTabs: [{
        name: 'Parents',
        properties: [
        {
          name: 'Father Face',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Father ancestry',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Mother Face',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Mother ancestry',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Ancestry dominant gene',
          value: 0,
          min: 1,
          max: 10
        }]
      },
      {
        name: 'Eyes',
        properties: [
        {
          name: 'Eye state',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Eye color',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Eyebrows',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Eyebrow color',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Brow width',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Brow shape',
          value: 0,
          min: 1,
          max: 10
        }]
      },{
        name: 'Nose',
        properties: [
        {
            name: 'Nose Width',
            value: 0,
            min: 1,
            max: 10
        },
        {
          name: 'Nose height',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Nose length',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Nose bridge shift',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Nose tip',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Nose shift',
          value: 0,
          min: 1,
          max: 10
        }]
      },
      {
        name: 'Chin',
        properties: [
        {
          name: 'Chin length',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Chin position',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Chin width',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Chin height',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Jaw width',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Jaw height',
          value: 0,
          min: 1,
          max: 10
        }]
      },
      {
        name: 'Cheek',
        properties: [
        {
          name: 'Cheekbone height',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Cheekbone width',
          value: 0,
          min: 1,
          max: 10
        },
        {
          name: 'Cheeks width',
          value: 0,
          min: 1,
          max: 10
        }]
      },
      {
        name: 'Lips',
        properties: [
        {
          name: 'Lips width',
          value: 0,
          min: 1,
          max: 10
        }]
      },
      {
        name: 'Neck',
        properties: [
        {
          name: 'Neck height',
          value: 0,
          min: 1,
          max: 10
        }]
      }]
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
