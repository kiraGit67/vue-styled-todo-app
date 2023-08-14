<template>
  <button class="button" id="delete-button" @click="deleteDoneToDos">
    {{ buttonText }}
  </button>
</template>

<script>
export default {
  name: "DeleteButton",
  props: {
    buttonText: String,
  },
  methods: {
    deleteDoneToDos() {
      this.$emit("deleteToDo");
    },
  },
};
</script>

<style scoped></style>
