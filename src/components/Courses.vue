<template>
  <div>
    <h1 class="title">Courses</h1>
    <table id="courses">
      <thead>
        <tr>
          <th>#</th>
          <th>Course Title</th>
          <th>Semester</th>
          <th>Grade</th>
        </tr>
      </thead>
      <tbody>
          <!-- Järgnev koodijupp loob tsükliga tabeli, võttes andmed completedCourses arrayst. -->
        <tr v-for="(course, index) in completedCourses" :key="index.id">
          <td>{{index+1}}</td>
          <td>{{course.title}}</td>
          <td>{{course.semester}}</td>
          <td>{{course.grade}}</td>
        </tr>
      </tbody>
    </table>
    <br />
    <br />
    <div>
        <!-- Antud on boolean addButtonClicked, mis iga "+" nuppu vajutamise järel 
        muudab väärtust. Kui väärtus on true siis näidatakse kasutajale uue kursuse
        sisestusvormi.  -->
      <button
        id="add-course-button"
        class="blue-button"
        @click="addButtonClicked=!addButtonClicked"
      >+</button>
      <span v-if="addButtonClicked" id="add-course">
        <input class="input" v-model="title" type="text" placeholder="Course title" id="title" />
        <input
          class="input"
          v-model="semester"
          type="number"
          min="1"
          max="8"
          placeholder="Semester"
          id="semester"
        />
        <input
          class="input"
          v-model="grade"
          type="number"
          min="0"
          max="100"
          placeholder="Grade"
          id="grade"
        />
        <button class="green-button" id="save-course" @click="addCourse">Save</button>
        <button class="grey-button" id="cancel-course" @click="addButtonClicked=false">Cancel</button>
      </span>
    </div>
  </div>
</template>

<script>
import Course from "../Course.js";
export default {
  name: "Courses",
  data: () => {
    return {
      title: "",
      grade: "",
      semester: "",
      completedCourses: [
        new Course("Agile software development", 1, 82),
        new Course("System modeling", 1, 85),
        new Course("Object-oriented programming", 2, 99),
        new Course("Estonian language level A2", 2, 65)
      ],
      addButtonClicked: false
    }
    
  },
  methods: {
    addCourse: function() {
      this.completedCourses.push(
        new Course(this.title, this.semester, this.grade)
      );
      this.title = "";
      this.semester = "";
      this.grade = "";
      this.addButtonClicked = false;
    }
  },
  props: {}
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

table th {
  padding: 8px 12px;
  text-align: left;
  border: 1px solid #cbcbcb;
  background-color: #03a9f4;
  color: #ffffff;
}

table td {
  padding: 8px 12px;
  border: 1px solid #cbcbcb;
}
.blue-button {
  background-color: #2196f3;
  color: #ffffff;
  border: none;
  padding: 10px 20px;
}

.green-button {
  background-color: #69f378;
  color: #ffffff;
  border: none;
  padding: 10px 10px;
}

.grey-button {
  background-color: #e1e8e6;
  color: #ffffff;
  border: none;
  padding: 10px 20px;
}

.input {
  border: 1px solid #cccccc;
  padding: 10px 20px;
  min-width: 135px;
}
</style>