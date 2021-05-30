<template>
      <Busses
        @filter-busses="filterBusses"
        @update-bus="updateBus" 
        @delete-bus="deleteBus" 
        @copy-bus="copyBus" 
        @add-bus="addBus" 
        :busses="busses" />
</template>

<script>
import _ from 'lodash';

import Busses from '../components/Busses';

export default {
  name: 'App',
  components: {
    Busses,
  },
  data() {
    return {
      busses: [],
    }
  },
  methods: {
    filterBusses(filters) {
      console.log('FILTERING', filters)
      const filterKeys = Object.keys(filters);
      for (let key of filterKeys) {
        if (_.get(filters[key], 'length')) {
          console.log(key, filters[key])
          this.busses = this.busses.filter(x => x[key] == filters[key]);
        }
      }
    },
    addBypass(busses) {
      console.log('Add', busses)
    },
    deleteBus(id) {
      console.log('delete ', id)
      this.busses = this.busses.filter(el => el.id !== id);
    },
    copyBus(id) {
      console.log('copy ', id)
      for (let bus of this.busses) {
        if (bus.id === id) {
          const newBus = {
            ...bus,
            id: Math.floor(Math.random()*100000)
          }
          this.busses.push(newBus);
        }
      }
    },
    updateBus(newBus) {
      for (let i = 0; i< this.busses.length; i++) {
        if (this.busses[i].id === newBus.id) {
          this.busses[i] = newBus;
        }
      }
    },
    addBus(bus) {
      console.log('add', bus)
      this.busses.push(bus);
    }
  },
  created() {
    this.busses = [
      {
          id: 1,
          number: 1,
          endLocation: 'BAM',
          make: 'Mercedes',
          startTime: '12:50'
        },
        {
          id: 2,
          number: 2,
          endLocation: 'BAM',
          make: 'Mercedes',
          startTime: '12:50'
        },
        {
          id: 3,
          number: 3,
          endLocation: 'BAM',
          make: 'Mercedes',
          startTime: '12:50'
        },
    ];
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
