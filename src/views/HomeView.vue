<template>
  <div class="home">
    <HelloWorld msg="test" />
    <FormTask @createtask="addTask" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import FormTask from "@/components/FormTask.vue";
import tasksService from "@/services/tasks.js";

export default {
  name: "HomeView",
  components: {
    HelloWorld,
    FormTask,
  },
  setup() {
    function addTask(data) {
      console.log("HomeView.vue | addTask()", data);
      tasksService.create(data);
    }
    return { addTask };
  },
};
</script>
