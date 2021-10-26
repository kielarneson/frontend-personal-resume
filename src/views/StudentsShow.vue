<template>
  <div class="students-show">
    <h2>{{ student }}</h2>
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
