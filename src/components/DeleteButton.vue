<template>
  <button class="button" id="delete-button">{{ buttonText }}</button>
</template>

<script>
export default {
  name: "DeleteButton",
  props: {
    buttonText: String,
  },
};
</script>

<style scoped></style>
