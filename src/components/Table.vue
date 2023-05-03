<template>
  <tr>
    <td><input type="text" v-model="data.task.name" /></td>
    <td v-for="(cell, cellIndex) in data.dates" :key="cell.id">
      <div v-if="!cell.isActive">
        <button @click="onCellClick(cellIndex)">+</button>
      </div>
      <div v-else>
        <select
          v-model="cell.status"
          @change="onCellChange(cellIndex)"
        >
          <option
            v-for="(elStatus, i) in this.data.statuses"
            :key="i"
          >
            {{ elStatus.status }}
          </option>
        </select>
      </div>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
  methods: {
    generateId() {
      this.uuid = Math.floor(Math.random() * 100000);
      this.localId = Math.floor(Math.random() * 100000);
    },
    onCellClick(cellIndex) {
      this.data.dates[cellIndex].isActive = true;

      console.log(
        `Button clicked in cell ${
          cellIndex + 1
        }. Selected option: ${this.data.dates[cellIndex].date}`
      );
    },
    onCellChange(cellIndex) {
      this.generateId();
      console.log(this.data.dates[cellIndex].status);
      console.log(
        `Button clicked in cell ${
          cellIndex + 1
        }. Selected option: ${this.data.dates[cellIndex].date}`
      );
      const index = this.data.events.findIndex(
        (item) => item.date === this.data.dates[cellIndex].date
      );
      if (index === -1) {
        let eventData = {
          id: this.uuid,
          name: this.data.task.name,
          date: this.data.dates[cellIndex].date,
          status: this.data.dates[cellIndex].status,
        };
        this.data.events.push(eventData);
      } else {
        this.data.events[index].status =
          this.data.dates[cellIndex].status;
      }
    },
  },
};
</script>
