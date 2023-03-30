<template>
  <main>
    <div class="home">
      <h1 v-if="NY">{{ students }}</h1>
      <h1 v-else>this student is not in NY</h1>
    </div>
    <TheWelcome />
  </main>
</template>

<style>
h1 {
  color: blue;
}
</style>

<script setup>
import TheWelcome from "../components/TheWelcome.vue";

export default {
  name: "home",
  components: {},
  data() {
    return {
      students: "Leon",
      state: "NY",
    };
  },
};
</script>
