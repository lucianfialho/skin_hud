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
        properties: [{
         name: 'Father Face',
         value: 0 
        },
        {
         name: 'Father ancestry',
         value: 0 
        },
        {
         name: 'Mother Face',
         value: 0 
        },
        {
         name: 'Mother ancestry',
         value: 0 
        },
        {
         name: 'Ancestry dominant gene',
         value: 0 
        }]
      },
      {
        name: 'Eyes',
        properties: [{
         name: 'Eye state',
         value: 0 
        },
        {
         name: 'Eye color',
         value: 0 
        },
        {
         name: 'Eyebrows',
         value: 0 
        },
        {
         name: 'Mother ancestry',
         value: 0 
        },
        {
         name: 'Ancestry dominant gene',
         value: 0 
        }]
      },{
        name: 'Nose'
      },
      {
        name: 'Chin'
      },
      {
        name: 'Cheek'
      },
      {
        name: 'Lips'
      },
      {
        name: 'Neck'
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
