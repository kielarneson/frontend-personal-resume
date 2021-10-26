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
      message: "test",
    };
  },
  created: function () {
    axios.get("/students/" + this.$route.params.id).then((response) => {
      console.log("students-show", response);
      this.student = response.data;
    });
  },
  methods: {},
};
</script>
