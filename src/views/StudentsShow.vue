<template>
  <div class="students-show">
    <h2>{{ student.first_name }} {{ student.last_name }}</h2>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      student: {},
    };
  },
  created: function () {
    axios.get("/https://afternoon-reaches-14167.herokuapp.com/students").then((response) => {
      this.student = response.data;
    });
  },
  methods: {},
};
</script>
