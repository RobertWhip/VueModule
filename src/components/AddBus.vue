<template>
  <tr>
    <td><input type="text" v-model="number"></td>
    <td><input type="text" v-model="endLocation"></td>
    <td><input type="text" v-model="make"></td>
    <td><input type="text" v-model="startTime"></td>
    <td> 
      <table>
        <tr>
          <th><button @click="onSubmit">Додати</button></th>
        </tr>
      </table>
    </td>
  </tr>
</template>

<script>
export default {
    name: 'AddBus',
    data() {
        return {
            number: '',
            endLocation: '',
            make: '',
            startTime: '',
        }
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();

            const bus = {
                id: Math.floor(Math.random()*100000),
                number: this.number,
                endLocation: this.endLocation,
                make: this.make,
                startTime: this.startTime,
            };

            this.$emit('add-bus', bus);
            
            this.number = '';
            this.endLocation = '';
            this.make = '';
            this.startTime = '';
        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>