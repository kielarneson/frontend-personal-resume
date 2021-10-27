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
    let student_id = localStorage.getItem("student_id");
    axios.get(`https://afternoon-reaches-14167.herokuapp.com/students/${student_id}`).then((response) => {
      console.log("Student Show", response);
      this.student = response.data;
    });
  },
  methods: {},
};
</script>
