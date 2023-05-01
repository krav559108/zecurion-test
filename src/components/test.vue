<template>
    <table>
      <tr v-for="(row, rowIndex) in tableData" :key="rowIndex">
        <td v-for="(cell, cellIndex) in row" :key="cellIndex">
          <div v-if="!cell.clicked">
            <button @click="onCellClick(rowIndex, cellIndex)">{{ cell.value }}</button>
          </div>
          <div v-else>
            <select v-model="cell.value" @change="onCellChange(rowIndex, cellIndex)">
              <option value="yes">Yes</option>
              <option value="no">No</option>
            </select>
          </div>
        </td>
      </tr>
    </table>
  </template>
  
  <script>
  export default {
    data() {
      return {
        tableData: [
          [
            { value: "Cell 1-1", clicked: false },
            { value: "Cell 1-2", clicked: false }
          ],
          [
            { value: "Cell 2-1", clicked: false },
            { value: "Cell 2-2", clicked: false }
          ]
        ]
      };
    },
    methods: {
      onCellClick(rowIndex, cellIndex) {
        this.tableData[rowIndex][cellIndex].clicked = true;
      },
      onCellChange(rowIndex, cellIndex) {
        console.log(
          `Button clicked in cell ${rowIndex + 1}-${cellIndex + 1}. Selected option: ${this.tableData[rowIndex][cellIndex].value}`
        );
      }
    }
  };
  </script>
  
  <style>
  table {
    border-collapse: collapse;
  }
  td {
    border: 1px solid black;
    padding: 5px;
  }
  select {
    width: 100%;
  }
  </style>
  