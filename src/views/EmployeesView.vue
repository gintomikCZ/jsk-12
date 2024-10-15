<template>

  <h1>list of employees</h1>
  <RouterLink to="/">home</RouterLink>

  <!-- <ul v-if="!loading">
    <li v-for="employee in employees">{{ employee.firstname + ' ' + employee.lastname }}</li>
  </ul> -->
  <TTable v-if="!loading" :headers="headers" :tableData="employeesToDisplay"/>

  <div v-else>... loading ...</div>
  <div>{{  fullName  }}</div>
</template>

<script>
import axios from 'axios'
import TTable from '@/components/TTable.vue'

export default {
  name: 'EmployeesView',
  data () {
    return {
      first: 'Karel',
      last: 'Houska',
      employees: [],
      loading: true,
      headers: ['first name', 'last name', 'date of birth', 'position', 'salary']
    }
  },
  computed: {
    fullName () {
      return this.first + ' ' + this.last
    },
    employeesToDisplay () {
      if (this.loading) {
        return []
      }
      return this.employees.map((employee) => {
        return {
          firstname: employee.firstname,
          lastname: employee.lastname,
          dateofbirth: employee.dateofbirth,
          position: employee.position,
          salary: employee.salary
        }
      })
    }
  },
  created () {
    axios.get('https://sdaapi.glabazna.eu/employees')
      .then((response) => {
        this.employees = response.data.data
        this.loading = false
      })
  },
  components: { TTable }
}

</script>