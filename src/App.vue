<template>
  <div id="app">
    <h1>Natural Events</h1>
    <h2>The Earth Observatory Natural Event Tracker (EONET)</h2>
    <li v-for="(title, value) in eventData">
          <span>{{ title }}</span>
        </li>
  </div>
</template>

<script>
import {eventBus} from './main.js'

export default {
  name: 'app',
  data() {
    return {
      eventData: []

    }
  },

  mounted(){
    fetch('https://eonet.sci.gsfc.nasa.gov/api/v2.1/events')
    .then(response => response.json())
    .then(res => this.eventData = this.transformEvents(res.events))

  },
  methods: {
    transformEvents(arr){
      return arr.map((event) => {
        return [event.title, event.description, event.link, event.categories, event.sources, event.geometries]
      })
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: left;
  color: #000000;
  margin-top: 60px;
}
</style>
