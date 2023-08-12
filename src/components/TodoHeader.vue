<template>
  <header class="header">
    <h1 class="header__title">{{ headerTitle }}</h1>
  </header>
</template>

<script>
export default {
  name: "TodoHeader",
  props: {
    headerTitle: String,
  },
};
</script>

<style scoped>
.header {
  text-align: center;
  background-color: var(--pink);
  padding: 3rem 1rem;
  color: white;
  margin-bottom: 1rem;
}

.header__title {
  margin: 0;
  text-shadow: 2px 2px var(--light-blue), 4px 4px var(--yellow);
}
</style>
