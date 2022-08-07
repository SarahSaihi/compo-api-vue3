<template>
  <h3>Créer une tâche</h3>
  <form @submit.prevent="createTask">
    <input
      type="text"
      placeholder="Nom de la tâche"
      v-model="name"
      ref="txtName"
    />
    <br />
    <textarea
      cols="30"
      rows="10"
      v-model="description"
      placeholder="Description"
    ></textarea
    ><br />
    <select v-model="temporality">
      <option
        v-for="tempo in temporalityTypes"
        :value="tempo.value"
        :key="tempo.id"
      >
        {{ tempo.name }}
      </option></select
    ><br />
    <button :disabled="!isFormValid">créer</button>
  </form>
</template>

<script>
import { ref, onMounted, computed } from "vue";

export default {
  name: "FormTask",
  emits: ["createtask"],
  setup(props, context) {
    const name = ref("");
    const description = ref("");
    const temporalityTypes = ref([
      {
        id: 1,
        name: "court terme",
        value: "short-term",
      },
      {
        id: 2,
        name: "moyen terme",
        value: "medium-term",
      },
      {
        id: 3,
        name: "long terme",
        value: "long-term",
      },
    ]);
    const temporality = ref("");
    let txtName = ref(null);

    function createTask() {
      const task = {
        id: Date.now(),
        name: name.value,
        description: description.value,
        temporality: temporality.value,
      };
      console.log("task", task);
      context.emit("createtask", task);
      resetForm();
    }

    function resetForm() {
      name.value = "";
      description.value = "";
      temporality.value = "";
      txtName.value.focus();
    }

    onMounted(() => {
      txtName.value.focus();
    });

    const isFormValid = computed(() => {
      if (
        name.value !== "" &&
        description.value !== "" &&
        temporality.value !== ""
      ) {
        return true;
      } else {
        return false;
      }
    });
    return {
      name,
      description,
      temporalityTypes,
      temporality,
      createTask,
      txtName,
      isFormValid,
    };
  },
};
</script>

<style scoped>
input,
textarea,
select,
button {
  width: 90%;
  margin: 5px 10px;
}
</style>
