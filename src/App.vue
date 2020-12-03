<template>
  <div id="app">
    <Kanban :data="data"/>
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
          tasks:[]
        },
        {
          name:"doing",
          color:"#C0FB84",
          tasks:[]
        },
        {
          name:"done",
          color:"#F69D9D",
          tasks:[]
        },
      ]
    }
  }
};
</script>

<style>
#app {
  height: 100vh;
}
</style>
