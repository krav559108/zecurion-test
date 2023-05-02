<template>
  <div>
    <div class="input">
      <div class="inputColumn">
        <span>Добавить задачу</span>
        <input name="text" placeholder="Введите задачу" v-model="task" />
        <button @click="addTask">Добавить</button>
        <div v-for="(e, i) in this.data" :key="i">
          {{ `${e.task.id} ${e.task.name}` }}
        </div>
      </div>
      <div class="inputColumn">
        <span>Добавить дату</span>
        <input name="date" placeholder="dd-mm-yyyy" v-model="date" />
        <button @click="addDate">Добавить</button>
        <div v-for="(e, i) in this.data[0].dates" :key="i">
          {{ `${e.id} ${e.date}` }}
        </div>
      </div>
      <div class="inputColumn">
        <span>Добавить статус</span>
        <input name="text" placeholder="Введите статус" v-model="status" />
        <button @click="addStatus">Добавить</button>
        <div v-for="(el, i) in this.data[0].statuses" :key="i">
          {{ `${el.id} ${el.status}` }}
        </div>
      </div>
      <div class="inputColumn">
        <span>Задачи со статусом</span>
        <div v-for="(el, i) in this.data" :key="i">
          <div v-for="(event, j) in el.events" :key="j">
            {{
              event.id +
              " " +
              el.task.name +
              " " +
              event.date +
              " " +
              event.status
            }}
          </div>
        </div>
      </div>
    </div>
    <table>
      <tbody>
        <tr>
          <td>Задачи / Даты</td>
          <td v-for="(el, i) in this.data[0].dates" :key="i">{{ el.date }}</td>
        </tr>
        <tr v-for="(row, rowIndex) in this.data" :key="row.id">
          <td><input type="text" v-model="row.task.name" /></td>
          <td v-for="(cell, cellIndex) in row.dates" :key="cell.id">
            <div v-if="!cell.isActive">
              <button @click="onCellClick(rowIndex, cellIndex)">+</button>
            </div>
            <div v-else>
              <select
                v-model="cell.status"
                @change="onCellChange(rowIndex, cellIndex)"
              >
                <option
                  v-for="(elStatus, i) in this.data[rowIndex].statuses"
                  :key="i"
                >
                  {{ elStatus.status }}
                </option>
              </select>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  components: {},
  props: {
    data: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
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
    onCellClick(rowIndex, cellIndex) {
      this.data[rowIndex].dates[cellIndex].isActive = true;

      console.log(
        `Button clicked in cell ${rowIndex + 1}-${
          cellIndex + 1
        }. Selected option: ${this.data[rowIndex].dates[cellIndex].date}`
      );
    },
    onCellChange(rowIndex, cellIndex) {
      this.generateId();
      console.log(this.data[rowIndex].dates[cellIndex].status);
      console.log(
        `Button clicked in cell ${rowIndex + 1}-${
          cellIndex + 1
        }. Selected option: ${this.data[rowIndex].dates[cellIndex].date}`
      );
      const index = this.data[rowIndex].events.findIndex(
        (item) => item.date === this.data[rowIndex].dates[cellIndex].date
      );
      if (index === -1) {
        let eventData = {
          id: this.uuid,
          name: this.data[rowIndex].task.name,
          date: this.data[rowIndex].dates[cellIndex].date,
          status: this.data[rowIndex].dates[cellIndex].status,
        };
        this.data[rowIndex].events.push(eventData);
      } else {
        this.data[rowIndex].events[index].status =
          this.data[rowIndex].dates[cellIndex].status;
      }
    },
    getDates() {
      this.data.forEach((e) =>
        e.dates.forEach((d) =>
          this.dates.push({
            id: d.id,
            date: d.date,
          })
        )
      );
    },
    getStatuses() {
      this.data.forEach((e) =>
        e.statuses.forEach((s) => this.statuses.push(s))
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
        this.data.push(dataSetTask);
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
        this.data.forEach((e) => {
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
        this.data.forEach((e) => {
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
};
</script>

<style>
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
