<template>
  <div class="students-show">
    
    <!-- ======= Resume Section ======= -->
<section id="resume" class="resume">
  <div class="container">

    <div class="section-title">
      <h2>Resume</h2>
      <p>Check My Resume</p>
    </div>

    <div class="row">
      <div class="col-lg-6">
        <h3 class="resume-title">Sumary</h3>
        <div class="resume-item pb-0">
          <h4>Alice Barkley</h4>
          <p><em>Innovative and deadline-driven Graphic Designer with 3+ years of experience designing and developing user-centered digital/print marketing material from initial concept to final, polished deliverable.</em></p>
          <p>
          <ul>
            <li>Portland par 127,Orlando, FL</li>
            <li>(123) 456-7891</li>
            <li>alice.barkley@example.com</li>
          </ul>
          </p>
        </div>

        <h3 class="resume-title">Education</h3>
        <div class="resume-item">
          <h4>Master of Fine Arts &amp; Graphic Design</h4>
          <h5>2015 - 2016</h5>
          <p><em>Rochester Institute of Technology, Rochester, NY</em></p>
          <p>Qui deserunt veniam. Et sed aliquam labore tempore sed quisquam iusto autem sit. Ea vero voluptatum qui ut dignissimos deleniti nerada porti sand markend</p>
        </div>
        <div class="resume-item">
          <h4>Bachelor of Fine Arts &amp; Graphic Design</h4>
          <h5>2010 - 2014</h5>
          <p><em>Rochester Institute of Technology, Rochester, NY</em></p>
          <p>Quia nobis sequi est occaecati aut. Repudiandae et iusto quae reiciendis et quis Eius vel ratione eius unde vitae rerum voluptates asperiores voluptatem Earum molestiae consequatur neque etlon sader mart dila</p>
        </div>
      </div>
      <div class="col-lg-6">
        <h3 class="resume-title">Professional Experience</h3>
        <div class="resume-item">
          <h4>Senior graphic design specialist</h4>
          <h5>2019 - Present</h5>
          <p><em>Experion, New York, NY </em></p>
          <p>
          <ul>
            <li>Lead in the design, development, and implementation of the graphic, layout, and production communication materials</li>
            <li>Delegate tasks to the 7 members of the design team and provide counsel on all aspects of the project. </li>
            <li>Supervise the assessment of all graphic materials in order to ensure quality and accuracy of the design</li>
            <li>Oversee the efficient use of production project budgets ranging from $2,000 - $25,000</li>
          </ul>
          </p>
        </div>
        <div class="resume-item">
          <h4>Graphic design specialist</h4>
          <h5>2017 - 2018</h5>
          <p><em>Stepping Stone Advertising, New York, NY</em></p>
          <p>
          <ul>
            <li>Developed numerous marketing programs (logos, brochures,infographics, presentations, and advertisements).</li>
            <li>Managed up to 5 projects or tasks at a given time while under pressure</li>
            <li>Recommended and consulted with clients on the most appropriate graphic design</li>
            <li>Created 4+ design presentations and proposals a month for clients and account managers</li>
          </ul>
          </p>
        </div>
      </div>
    </div>

  </div>
</section><!-- End Resume Section -->
    
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
      <!-- LinkenIn:
      <input type="text" v-model="student.linkedin_url" />
      Twitter:
      <input type="text" v-model="student.twitter_handle" />
      Github:
      <input type="text" v-model="student.github_url" />
      Blog:
      <input type="text" v-model="student.personal_blog" /> -->
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
