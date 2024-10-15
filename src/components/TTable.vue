<template>
<!-- zobrazit jednořádkovou hlavičku tabulky -->
<!-- zobrazit všechny data, která dostane v tabulce -->

  <table>
    <thead>
      <tr>
        <th v-for="item in headers">{{ item }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in tableData">
        <td
          v-for="property in Object.keys(item)"
          :class="{
            'text-left': typeof item[property] === 'string',
            'text-right': typeof item[property] === 'number' && !Number.isNaN(item[property])
          }"
        >{{ item[property] }}</td>
      </tr>
    </tbody>
  </table>

</template>

<script>

/*
Object.keys(obj) => vrací pole s názvy klíčů

const obj = {
  name: 'Karel',
  position: 'driver',
  salary: 5000
}

console.log(obj.name)
console.log(obj.position)
console.log(obj.salary)

const propertyIWantToKnow = 'name'

console.log(obj[propertyIWantToKnow]) // 'Karel'


*/


export default {
  name: 'TTable',
  props: {
    headers: {
      type: Array
    },
    tableData: {
      type: Array
    }
  }
}

</script>

<style scoped>
  table {
    border-collapse: collapse;
  }
  td, th {
    border: 1px solid #cdcdcd;
    padding: .3em .6em;
  }
  th {
    font-weight: bold;
    background: lightpink;
  }
  .text-left {
    text-align: left;
  }
  .text-right {
    text-align: right;
  }
</style>