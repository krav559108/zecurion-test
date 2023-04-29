<template>
  <table>
    <tbody>
      <tr>
        <td>Задачи</td>
        <td v-for="(date, i) in dates" :key="i"> {{date}}</td>
      </tr>
      <tr v-for="(task, i) in tasks" :key="i" >
        <td>{{task}}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    tasks: {
      type: Array,
      required: true,
    },
    dates: {
      type: Array,
      required: true,
    },
    statuses: {
      type: Array,
      required: true,
    },
    data() {
      return {
        // tasks:[],
        // dates:[],
        // statuses:[],
      };
    },
    computed: {},
  },
};
</script>

<style>
table {
  margin: auto;
}
table,
td {
  padding: 3px;
  border: 1px solid #333;
}
th {
  padding: 5px;
}

</style>
