<template>
  <div class="students-show">
    <h1>{{ student.name }}</h1>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
    };
  },
  created: function () {
    axios.get("/");
  },
  methods: {},
};
</script>
