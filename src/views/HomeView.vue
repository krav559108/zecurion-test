<template>
  <InputData></InputData>
  <!-- <Table :tasks="tasks" :dates="dates" :statuses="statuses"></Table> -->
</template>

<script>
import InputData from "@/components/InputData.vue";
import Table from "@/components/Table.vue";

export default {
  name: "App",
  components: {
    InputData,
    Table,
  },
  data() {
    return {
      tasks: ["Задача 1", "Задача 2", "Задача 3"],
      dates: ["13.03", "20.03", "27.03", "03.04", "10.04"],
      statuses: ["Готово", "Не готово", "В работе", "На проверке"],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
