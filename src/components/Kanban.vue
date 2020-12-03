<template>
  <div class="kanban">
    <div
      class="culumn"
      :style="{ backgroundColor: column.color }"
      v-for="(column, index) in data"
      :key="index"
    >
      <div class="colum-header">
        {{ column.name }}
      </div>
      <div class="column-body">
        <div class="create-task" @click="create_task(index)">Create task</div>
      </div>
    </div>
    <b-modal ref="create-task-modal" title="Create Task">
      <p class="my-4">Hello from modal!</p>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    data: Array,
  },
  methods: {
    create_task(index_column) {
      console.log(index_column);
      this.$refs["create-task-modal"].show();
    },
  },
};
</script>

<style>
.kanban {
  width: 100%;
  height: 100%;
  background-color: rgb(210, 162, 255);
}
.culumn {
  height: 600px;
  width: 300px;
  border-radius: 30px;
  display: inline-block;
  margin: 25px;
  -webkit-box-shadow: 21px 21px 18px -7px rgba(0, 0, 0, 0.61);
  -moz-box-shadow: 21px 21px 18px -7px rgba(0, 0, 0, 0.61);
  box-shadow: 21px 21px 18px -7px rgba(0, 0, 0, 0.61);
  padding: 18px;
}
.colum-header {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px;
  font-size: 32px;
  font-weight: bold;
}
.column-body {
  height: calc(100% - 50px);
  border-radius: 10px;
  padding: 5px;
  background-color: #b9c1f0a2;
}
.create-task {
  widows: 100%;
  height: auto;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
}
.create-task:hover {
  background-color: cornflowerblue;
}
</style>