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
        <div v-for="(task, task_index) in column.tasks" :key="task_index">
          <div
            class="task"
            :draggable="true"
            @dragstart="start_move(task_index, index)"
          >
            {{ task.task_name }}
          </div>
          <div
            class="drop_zone"
            @dragenter.prevent="drop_zone_enter"
            @dragleave.prevent="drop_zone_leave"
            @dragover.prevent
          ></div>
        </div>

        <div class="create-task" @click="create_task(index)">Create task</div>
      </div>
    </div>
    <b-modal ref="create-task-modal" title="Create Task">
      <input
        class="input-task-name"
        v-model="task_name"
        @keyup.13="submit_create_task"
      />
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    data: Array,
    create_task_submit: Function,
  },
  methods: {
    create_task(index_column) {
      this.current_column_index = index_column;
      this.$refs["create-task-modal"].show();
    },
    submit_create_task() {
      this.create_task_submit(this.current_column_index, {
        task_name: this.task_name,
      });
    },
    start_move(task_index, current_column_index) {
      this.current_column_index = current_column_index;
      this.current_task_index = task_index;
    },
    drop_zone_enter(event) {
      event.target.style.height = "100px";
      event.target.style.borderStyle = "dotted";
      event.target.style.transition = "height 0.5s";
    },

    drop_zone_leave(event) {
      event.target.style.height = "10px";
      event.target.style.borderStyle = "none";
      event.target.style.transition = "height 0.5s";
    },
  },
  data() {
    return {
      task_name: "",
      current_column_index: "",
      current_task_index: "",
    };
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
.input-task-name {
  width: 100%;
}
.task {
  position: relative;
  width: auto;
  height: 100px;
  border-radius: 2px;
  margin: 10px;
  background-color: #d8fd95;
}
.drop_zone {
  height: 10px;
}
</style>