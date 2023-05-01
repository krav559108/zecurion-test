<template>
  <InputData :data="tableData"></InputData>
</template>

<script>
import InputData from "@/components/InputData.vue";

export default {
  name: "App",
  components: {
    InputData,

  },
  data() {
    return {
      tableData: [
        {
          id: 1,
          task: {
            id: 1,
            name: "Задача 1",
          },
          dates: [
            { id: 4, date: "13.03", isActive: false, status:"" },
            { id: 5, date: "20.03", isActive: false, status:""},
            { id: 6, date: "27.03", isActive: false, status:"" },
            { id: 7, date: "03.04", isActive: false, status:"" },
            { id: 8, date: "10.04", isActive: false, status:"" },
          ],
          statuses: [
            { id: 9, status: "Готово" },
            { id: 10, status: "Не готово" },
            { id: 11, status: "В работе" },
            { id: 12, status: "На проверке" },
          ],
          events: [
            {
              id: 1,
              name: "Задача 1",
              date: "27.03",
              status: "Готово",
            },
            {
              id: 1,
              name: "Задача 1",
              date: "03.04",
              status: "В работе",
            },
          ],
        },
      ],
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
