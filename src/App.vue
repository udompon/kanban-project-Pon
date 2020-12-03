<template>
  <div id="app">
    <Kanban :data="data" :create_task_submit=" create_task_submit"/>
  </div>
</template>

<script>
import Kanban from "./components/Kanban";

export default {
  name: "App",
  components: {
    Kanban,
  },
  data (){
    return{
      data:[
        {
          name:"todo",
          color:"#84FBF7",
          tasks:[{
            task_name: "tesk"
          }]
        },
        {
          name:"doing",
          color:"#C0FB84",
          tasks:[{
            task_name: "tesk"
          }]
        },
        {
          name:"done",
          color:"#F69D9D",
          tasks:[{
            task_name: "tesk"
          }]
        },
      ]
    }
  },
  methods:{
    create_task_submit(column_index,item){
      this.data[column_index].tasks.push(item)

    }
  }
};
</script>

<style>
#app {
  height: 100vh;
}
</style>
