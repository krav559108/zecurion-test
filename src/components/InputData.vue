<template>
  <div class="table">
    <div class="tableColumn">
      <span>Добавить задачу</span>
      <input name="text" placeholder="Введите задачу" v-model="task" />
      <button @click="addTask" value="Добавить"></button>
      <div>{{ taskData }}</div>
    </div>
    <div class="tableColumn">
      <span>Добавить дату</span>
      <input name="date" placeholder="dd-mm-yyyy" v-model="date" />
      <button @click="addDate" value="Добавить"></button>
      <div>{{ dateData }}</div>
    </div>
    <div class="tableColumn">
      <span>Добавить статус</span>
      <input name="text" placeholder="Введите статус"  v-model="status" />
      <button @click="addStatus" value="Добавить"></button>
      <div>{{ statusData }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: "",
      date: "",
      status: "",
      uuid: "",
      tasks: [],
      dates: [],
      statuses: [],
    };
  },
  methods: {
    generateId() {
      this.uuid = this.uuid + 1;
    },
    addTask() {
      if (this.task) {
        this.tasks.push(this.task);
        this.task = "";
      }
    },
    addDate() {
      if (this.date) {
        this.dates.push(this.date);
        this.date = "";
      }
    },
    addStatus() {
      if (this.status) {
        this.statuses.push(this.status);
        this.status = "";
      }
    },
  },
  computed: {
    taskData() {
      this.generateId() + " " + this.task;
    },
    dateData() { this.generateId() + " " + this.date; },
    statusData() {this.generateId() + " " + this.status;},
  },
};
</script>

<style>
.table {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.tableColumn {
  display: flex;
  flex-direction: column;
  padding: 1%;
}
</style>
