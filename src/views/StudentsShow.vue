<template>
  <div class="students-show">
    <!-- ======= About Section ======= -->
    <section id="about" class="about">
      <div class="container" data-aos="fade-up">
        <div class="section-title">
          <h2>
            {{ student.first_name }}
            {{ student.last_name }}
          </h2>
        </div>

        <div class="row">
          <div class="col-lg-4">
            <img src="assets/img/about.jpg" class="img-fluid" alt="" />
          </div>
          <div class="col-lg-8 pt-4 pt-lg-0 content">
            <h3>{{ student.experiences[0].job_title }}</h3>
            <p class="fst-italic">
              {{ student.experiences[0].details }}
            </p>
            <div class="row">
              <div class="col-lg-6">
                <ul>
                  <li>
                    <i class="bi bi-rounded-right"></i>
                    <strong>Website:</strong>
                    {{ student.personal_blog }}
                  </li>
                  <li>
                    <i class="bi bi-rounded-right"></i>
                    <strong>Phone:</strong>
                    {{ student.phone_number }}
                  </li>
                  <li>
                    <i class="bi bi-rounded-right"></i>
                    <strong>LinkedIn:</strong>
                    {{ student.linkedin_url }}
                  </li>
                  <li>
                    <i class="bi bi-rounded-right"></i>
                    <strong>Twitter:</strong>
                    {{ student.twitter_handle }}
                  </li>
                  <li>
                    <i class="bi bi-rounded-right"></i>
                    <strong>GitHub:</strong>
                    {{ student.github_url }}
                  </li>
                </ul>
              </div>
              <div class="col-lg-6">
                <ul>
                  <li v-for="education in educations" v-bind:key="education.id">
                    <i class="bi bi-rounded-right"></i>
                    <strong>Degree:</strong>
                    {{ education.degree }}
                  </li>
                  <li>
                    <i class="bi bi-rounded-right"></i>
                    <strong>Email:</strong>
                    {{ student.email }}
                  </li>
                  <li>
                    <i class="bi bi-rounded-right"></i>
                    <strong>Freelance:</strong>
                    Available
                  </li>
                </ul>
              </div>
            </div>
            <p>
              Officiis eligendi itaque labore et dolorum mollitia officiis optio vero. Quisquam sunt adipisci omnis et
              ut. Nulla accusantium dolor incidunt officia tempore. Et eius omnis. Cupiditate ut dicta maxime officiis
              quidem quia. Sed et consectetur qui quia repellendus itaque neque. Aliquid amet quidem ut quaerat
              cupiditate. Ab et eum qui repellendus omnis culpa magni laudantium dolores.
            </p>
          </div>
        </div>
      </div>
    </section>
    <!-- End About Section -->
    <h1>My Profile</h1>
    <div>
      First Name:
      <input type="text" v-model="student.first_name" />
      Last Name:
      <input type="text" v-model="student.last_name" />
    </div>

    <div>
      Email:
      <input type="text" v-model="student.email" />
      Phone Number:
      <input type="text" v-model="student.phone_number" />
    </div>

    <div>
      Bio:
      <input type="text" v-model="student.short_bio" />
    </div>

    <div>
      LinkenIn:
      <input type="text" v-model="student.linkedin_url" />
      Twitter:
      <input type="text" v-model="student.twitter_handle" />
      Github:
      <input type="text" v-model="student.github_url" />
      Blog:
      <input type="text" v-model="student.personal_blog" />
      Resume:
      <input type="text" v-model="student.online_resume_url" />
    </div>
    <button @click="updateStudent(student)">Update Student</button>

    <h3>Experience</h3>
    <div v-for="experience in experiences" v-bind:key="`experience-${experience.id}`">
      Company Name:
      <input type="text" v-model="experience.company_name" />
      Job Title:
      <input type="text" v-model="experience.job_title" />
      Start Date:
      <input type="text" v-model="experience.start_date" />
      End Date:
      <input type="text" v-model="experience.end_date" />
      Details:
      <input type="text" v-model="experience.details" />
      <button @click="updateExperience(experience)">Update Experience</button>
    </div>

    <h3>Education</h3>
    <div v-for="education in educations" v-bind:key="`education-${education.id}`">
      University Name:
      <input type="text" v-model="education.university_name" />
      Degree:
      <input type="text" v-model="education.degree" />
      Start Date:
      <input type="text" v-model="education.start_date" />
      End Date:
      <input type="text" v-model="education.end_date" />
      <button @click="updateEducation(education)">Update Education</button>
    </div>

    <h3>Projects</h3>
    <div v-for="project in projects" v-bind:key="`project-${project.id}`">
      Name:
      <input type="text" v-model="project.name" />
      Description:
      <input type="text" v-model="project.description" />
      Url:
      <input type="text" v-model="project.url" />
      <button @click="updateProject(project)">Update Project</button>
    </div>

    <h3>Skills</h3>
    <div v-for="skill in skills" v-bind:key="`skill-${skill.id}`">
      Skill:
      <input type="text" v-model="skill.skill_name" />
      <button @click="updateSkill(skill)">Update Skill</button>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      student: {},
      experiences: {},
      educations: {},
      projects: {},
      skills: {},
    };
  },
  created: function () {
    let student_id = localStorage.getItem("student_id");
    axios.get(`https://afternoon-reaches-14167.herokuapp.com/students/${student_id}`).then((response) => {
      console.log("Student Show", response);
      this.student = response.data;
      this.experiences = response.data.experiences;
      this.educations = response.data.educations;
      this.projects = response.data.projects;
      this.skills = response.data.skills;
    });
  },
  methods: {
    updateStudent: function (student) {
      let student_id = localStorage.getItem("student_id");
      var editStudentParams = student;
      axios
        .patch(`https://afternoon-reaches-14167.herokuapp.com/students/${student_id}`, editStudentParams)
        .then((response) => {
          console.log("student update", response);
        })
        .catch((error) => {
          console.log("profile update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
    updateExperience: function (experience) {
      var editExperienceParams = experience;
      axios
        .patch(`https://afternoon-reaches-14167.herokuapp.com/experiences/${experience.id}`, editExperienceParams)
        .then((response) => {
          console.log("Experience update", response);
        })
        .catch((error) => {
          console.log("profile update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
    updateEducation: function (education) {
      var editEducationParams = education;
      axios
        .patch(`https://afternoon-reaches-14167.herokuapp.com/educations/${education.id}`, editEducationParams)
        .then((response) => {
          console.log("Education update", response);
        })
        .catch((error) => {
          console.log("profile update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
    updateProject: function (project) {
      var editProjectParams = project;
      axios
        .patch(`https://afternoon-reaches-14167.herokuapp.com/projects/${project.id}`, editProjectParams)
        .then((response) => {
          console.log("Project update", response);
        })
        .catch((error) => {
          console.log("profile update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
    updateSkill: function (skill) {
      var editSkillParams = skill;
      axios
        .patch(`https://afternoon-reaches-14167.herokuapp.com/skills/${skill.id}`, editSkillParams)
        .then((response) => {
          console.log("Skill update", response);
        })
        .catch((error) => {
          console.log("profile update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
