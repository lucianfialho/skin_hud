<template>
  <div id="app">
    <section class="left-tabs">
      <b-tabs v-model="activeTab">
        <b-tab-item v-for="tab in leftTabs" v-bind:key="tab.id" :label="tab.name">
          {{tab.name}}
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
      leftTabs: [{
        name: 'Parents',
        properties: [
        {
          name: 'Father Face',
          value: 0,
          min: 1
        },
        {
          name: 'Father ancestry',
          value: 0,
          min: 1
        },
        {
          name: 'Mother Face',
          value: 0,
          min: 1
        },
        {
          name: 'Mother ancestry',
          value: 0,
          min: 1
        },
        {
          name: 'Ancestry dominant gene',
          value: 0,
          min: 1
        }]
      },
      {
        name: 'Eyes',
        properties: [
        {
          name: 'Eye state',
          value: 0,
          min: 1
        },
        {
          name: 'Eye color',
          value: 0,
          min: 1
        },
        {
          name: 'Eyebrows',
          value: 0,
          min: 1
        },
        {
          name: 'Eyebrow color',
          value: 0,
          min: 1
        },
        {
          name: 'Brow width',
          value: 0,
          min: 1
        },
        {
          name: 'Brow shape',
          value: 0,
          min: 1
        }]
      },{
        name: 'Nose',
        properties: [
        {
            name: 'Nose Width',
            value: 0,
            min: 1
        },
        {
          name: 'Nose height',
          value: 0,
          min: 1
        },
        {
          name: 'Nose length',
          value: 0,
          min: 1
        },
        {
          name: 'Nose bridge shift',
          value: 0,
          min: 1
        },
        {
          name: 'Nose tip',
          value: 0,
          min: 1
        },
        {
          name: 'Nose shift',
          value: 0,
          min: 1
        }]
      },
      {
        name: 'Chin',
        properties: [
        {
          name: 'Chin length',
          value: 0,
          min: 1
        },
        {
          name: 'Chin position',
          value: 0,
          min: 1
        },
        {
          name: 'Chin width',
          value: 0,
          min: 1
        },
        {
          name: 'Chin height',
          value: 0,
          min: 1
        },
        {
          name: 'Jaw width',
          value: 0,
          min: 1
        },
        {
          name: 'Jaw height',
          value: 0,
          min: 1
        }]
      },
      {
        name: 'Cheek',
        properties: [
        {
          name: 'Cheekbone height',
          value: 0,
          min: 1
        },
        {
          name: 'Cheekbone width',
          value: 0,
          min: 1
        },
        {
          name: 'Cheeks width',
          value: 0,
          min: 1
        }]
      },
      {
        name: 'Lips',
        properties: [
        {
          name: 'Lips width',
          value: 0,
          min: 1
        }]
      },
      {
        name: 'Neck',
        properties: [
        {
          name: 'Neck height',
          value: 0,
          min: 1
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
.left-tabs {
  width: 30%;
}
</style>
