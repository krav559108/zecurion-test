<template>
  <div class="table">
    <div class="tableColumn">
      <span>Добавить задачу</span>
      <input name="text" placeholder="Введите задачу" value="" />
      <input type="button" value="Добавить">
    </div>
    <div class="tableColumn">
      <span>Добавить дату</span>
      <input name="date" placeholder="dd-mm-yyyy" value="" />
      <input type="button" value="Добавить">
    </div>
    <div class="tableColumn">
      <span>Добавить статус</span>
      <input name="text" placeholder="Введите статус" value="" />
      <input type="button" value="Добавить">
    </div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            
        }
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
.tableColumn{
    display: flex;
    flex-direction: column;
    padding: 1%;
}
</style>
