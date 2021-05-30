<template>
    <div class="bus_table"  align="center">
      <table>
        <Filters @filter-busses="(filters) => $emit('filter-busses', filters)"/>
        <tr style="background-color: #42b983;">
          <th>№ Маршрута</th>
          <th>Кінцева зупинка</th>
          <th>Марка</th>
          <th>Час поїздки</th>
          <th></th>
        </tr>

        <tr :key="bus.id" v-for="bus in busses">
            <Bus 
                @update-bus="(bus) => $emit('update-bus', bus)"
                @delete-bus="$emit('delete-bus', bus.id)"
                @copy-bus="$emit('copy-bus', bus.id)"
                :bus="bus"/>
        </tr>
        <AddBus @add-bus="(bus) => $emit('add-bus', bus)"/>
      </table>
    </div>
</template>

<script>
import Bus from './Bus';
import AddBus from './AddBus';
import Filters from './Filters'

export default {
    name: 'Busses',
    props: {
        busses: Array,
    },
    components: {
        Bus,
        AddBus,
        Filters,
    },
    emits: ['delete-bus', 'copy-bus', 'update-bus', 'filter-busses']
}
</script>

<style scoped>
    th {
        width: 200px;
        height: 35px;
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