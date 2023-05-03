<template>
  <div>
    <div class="input">
      <div class="inputColumn">
        <span>Добавить задачу</span>
        <input name="text" placeholder="Введите задачу" v-model="task" />
        <button @click="addTask">Добавить</button>
        <div v-if="this.localData && this.localData.length > 0">
          <div class="dataColumn" v-for="e in this.localData" :key="e.id">
            {{ `${e.task.id} ${e.task.name}` }}
            <button @click="deleteDataItem(e.id)">X</button>
          </div>
        </div>
        <div v-else>Создайте задачу!</div>
      </div>
      <div class="inputColumn">
        <span>Добавить дату</span>
        <input name="date" placeholder="dd-mm-yyyy" v-model="date" />
        <button @click="addDate">Добавить</button>
        <div v-if="this.localData && this.localData.length > 0">
          <div
            class="dataColumn"
            v-for="(e, i) in this.localData[0].dates"
            :key="i"
          >
            {{ `${e.id} ${e.date}` }}
            <button @click="deleteDate(e.id)">X</button>
          </div>
        </div>
        <div v-else>Создайте задачу!</div>
      </div>
      <div class="inputColumn">
        <span>Добавить статус</span>
        <input name="text" placeholder="Введите статус" v-model="status" />
        <button @click="addStatus">Добавить</button>
        <div v-if="this.localData && this.localData.length > 0">
          <div
            class="dataColumn"
            v-for="(el, i) in this.localData[0].statuses"
            :key="i"
          >
            {{ `${el.id} ${el.status}` }}
            <button @click="deleteStatus(el.id)">X</button>
          </div>
        </div>
        <div v-else>Создайте задачу!</div>
      </div>
      <div class="inputColumn">
        <span>Задачи со статусом</span>
        <div v-if="this.localData && this.localData.length > 0">
          <div v-for="(el, i) in this.localData" :key="i">
            <div class="dataColumn" v-for="(event, j) in el.events" :key="j">
              {{
                event.id +
                " " +
                el.task.name +
                " " +
                event.date +
                " " +
                event.status
              }}
              <button @click="deleteTask(el.id, event.id)">X</button>
            </div>
          </div>
        </div>
        <div v-else>Создайте задачу!</div>
      </div>
    </div>
    <table v-if="this.localData && this.localData.length > 0">
      <tbody>
        <tr>
          <td>Задачи / Даты</td>
          <td v-for="(el, i) in this.localData[0].dates" :key="i">
            {{ el.date }}
          </td>
        </tr>

        <Table
          v-for="item in this.localData"
          :key="item.id"
          :data="item"
        ></Table>
      </tbody>
    </table>
    <div v-else>Создайте задачу!</div>
  </div>
</template>

<script>
import Table from "./Table.vue";
export default {
  components: { Table },
  props: {},
  data() {
    return {
      localData: [
        {
          id: 1,
          task: {
            id: 1,
            name: "Задача",
          },
          dates: [
            { id: 4, date: "13.03", isActive: false, status: "" },
            { id: 5, date: "20.03", isActive: false, status: "" },
            { id: 6, date: "27.03", isActive: false, status: "" },
            { id: 7, date: "03.04", isActive: false, status: "" },
            { id: 8, date: "10.04", isActive: false, status: "" },
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
      task: "",
      date: "",
      status: "",
      uuid: 0,
      localId: 0,
      tasks: [],
      dates: [],
      statuses: [],
      isActive: false,
    };
  },
  methods: {
    deleteDataItem(id) {
      const index = this.localData.findIndex((e) => e.id === id);
      if (index === 0) {
        this.localData = [];
      } else {
        this.localData = this.localData.splice(index, 1);
      }
    },
    deleteDate(id) {
      const index = this.localData[0].dates.findIndex((e) => e.id === id);
      this.localData.forEach((e) => e.dates.splice(index, 1));
    },
    deleteStatus(id) {
      const index = this.localData[0].statuses.findIndex((e) => e.id === id);
      this.localData.forEach((e) => e.statuses.splice(index, 1));
    },
    deleteTask(itemId, id) {
      const index = this.localData.findIndex((e) => e.id === itemId);
      const eventIndex = this.localData[index].events.findIndex(
        (e) => e.id === id
      );
      const date = this.localData[index].events[eventIndex].date;
      const dateIndex = this.localData[index].dates.findIndex(
        (e) => e.date === date
      );
      this.localData[index].dates[dateIndex].isActive = false;
      this.localData[index].dates[dateIndex].status = "";
      this.localData[index].events.splice(eventIndex, 1);
    },
    getDates() {
      this.localData.forEach((e) =>
        e.dates.forEach((d) =>
          this.dates.push({
            id: d.id,
            date: d.date,
          })
        )
      );
    },
    getStatuses() {
      this.localData.forEach((e) =>
        e.statuses.forEach((s) =>
          this.statuses.push({
            id: s.id,
            status: s.status,
          })
        )
      );
    },
    addTask() {
      this.generateId();
      let newDates = this.dates.map((e) => {
        return {
          id: e.id,
          date: e.date,
        };
      });
      if (this.task) {
        let dataSetTask = {
          id: this.uuid,
          task: {
            id: this.localId,
            name: this.task,
          },
          dates: newDates,
          statuses: this.statuses,
          events: [],
        };
        this.localData.push(dataSetTask);
        this.task = "";
      }
    },
    addDate() {
      this.generateId();
      if (this.date) {
        let dataSetDates = {
          id: this.uuid,
          date: this.date,
        };
        this.localData.forEach((e) => {
          e.dates.push(dataSetDates);
        });
        this.dates.push(dataSetDates);
        this.date = "";
      }
    },
    addStatus() {
      this.generateId();
      if (this.status) {
        let dataSetStatuses = {
          id: this.uuid,
          status: this.status,
        };
        this.localData.forEach((e) => {
          e.statuses.push(dataSetStatuses);
        });
        this.status = "";
      }
    },
    generateId() {
      this.uuid = Math.floor(Math.random() * 100000);
      this.localId = Math.floor(Math.random() * 100000);
    },
  },
  mounted() {
    this.getDates();
    this.getStatuses();
  },
  watch: {},
};
</script>

<style>
.dataColumn {
  display: flex;
  justify-content: space-between;
  padding-top: 3%;
}
span {
  padding-bottom: 15px;
}
.input {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.inputColumn {
  display: flex;
  flex-direction: column;
  padding: 1%;
}
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
