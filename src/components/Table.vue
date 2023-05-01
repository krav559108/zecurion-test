<template>

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
  },
  data() {
    return {
      taskTableData:[{task}],
    };
  },
  computed: {},
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
