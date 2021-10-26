<template>
  <div class="students-show">
    <h2>{{ student.first_name }} {{ student.last_name }}</h2>
  </div>
</template>

<style></style>

<script>
// import axios from "axios";
export default {
  data: function () {
    return {
      message: "test",
      student: { first_name: "Kiel", last_name: "Arneson" },
    };
  },
  created: function () {
    // axios.get("/students/" + this.$route.params.id).then((response) => {
    //   console.log("students-show", response);
    //   this.student = response.data;
    // });
    this.student;
  },
  methods: {},
};
</script>
