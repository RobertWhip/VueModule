<template>
    <tr>
        <td><input type="text" v-model="number" placeholder="№ Маршрута"></td>
        <td><input type="text" v-model="endLocation" placeholder="Кінцева зупинка"></td>
        <td><input type="text" v-model="make" placeholder="Марка"></td>
        <td><input type="text" v-model="startTime" placeholder="Час поїздки"></td>
        <td><button @click="onClick">Пошук</button></td>
    </tr>
</template>

<script>
export default {
    name: 'Bus',
    props: {
        bus: Object
    },
    data() {
      return {
        number: '',
        endLocation: '',
        make: '',
        startTime: '',
      }
    },
    methods: {
      onClick() {
        this.$emit('filter-busses', {
          number: this.number,
          endLocation: this.endLocation,
          make: this.make,
          startTime: this.startTime,
        })
        console.log('filter', {
          number: this.number,
          endLocation: this.endLocation,
          make: this.make,
          startTime: this.startTime,
        })
      }
    }
}
</script>

<style scope>
    .fas {
      color: red;
    }
    td {
        text-align:center;
    }

    input {
        outline: 0;
        border-width: 0 0 2px;
        border-color: black
    }
    input:focus {
        border-color: #42b983;
    }
</style>