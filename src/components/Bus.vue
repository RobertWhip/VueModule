<template>
  <td v-show="!edit">{{bus.number}}</td>
  <td v-show="!edit">{{bus.endLocation}}</td>
  <td v-show="!edit">{{bus.make}}</td>
  <td v-show="!edit">{{bus.startTime}}</td>
  <td v-show="edit"><input type="text" v-model="number" ></td>
  <td v-show="edit"><input type="text" v-model="endLocation" ></td>
  <td v-show="edit"><input type="text" v-model="make" ></td>
  <td v-show="edit"><input type="text" v-model="startTime" ></td>
  <td> 
    <table>
      <tr v-show="!edit">
          <td><button @click="$emit('copy-bus')">+</button></td>
          <td><button @click="editClick">Змінити</button></td>
          <td><button @click="$emit('delete-bus')">X</button></td>
      </tr>
      <tr v-show="edit">
          <td><button @click="saveClick">Зберегти</button></td>
      </tr>
    </table>
  </td>
</template>

<script>
export default {
    name: 'Bus',
    props: {
        bus: Object
    },
    data() {
      return {
        edit: false,
        number: '',
        endLocation: '',
        make: '',
        startTime: '',
      }
    },
    methods: {
      editClick() {
        console.log('click edit')
        this.edit = true;
      },
      saveClick() {
        this.$emit('update-bus', {
          id: this.bus.id,
          number: this.number,
          endLocation: this.endLocation,
          make: this.make,
          startTime: this.startTime,
        })
        console.log({
          id: this.bus.id,
          number: this.number,
          endLocation: this.endLocation,
          make: this.make,
          startTime: this.startTime,
        })
        this.edit = false;
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