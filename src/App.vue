<template>
  <main id="app">
    <Header />
    <section id="container">
      <section id="main">
        <div id="tabs">
          <div class="content">
              <!-- Tab-i valikuga muutub container sisuks olev komponent.  -->
            <div v-if="activetab === 1">
              <Profile :allCourses="allCourses" />
            </div>
            <div v-if="activetab === 2">
              <Courses :allCourses="allCourses" />
            </div>
          </div>
          <div class="tabs">
              <!-- Tab-ile klikates muutub see aktiivseks. class on active, kui tingimus activetab===1 on tõene. -->
            <a @click="activetab=1" v-bind:class="[ activetab === 1 ? 'active' : '' ]">Profile</a>
            <a @click="activetab=2" v-bind:class="[ activetab === 2 ? 'active' : '' ]">Courses</a>
          </div>
        </div>
      </section>
    </section>
    <Footer />
  </main>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Profile from "./components/Profile";
import Courses from "./components/Courses";
import Course from "./Course.js";
export default {
  name: "app",
  data: () => {
    return {
      activetab: 1,
      allCourses: [
        new Course("Agile software development", 1, 82),
        new Course("System modeling", 1, 85),
        new Course("Object-oriented programming", 2, 99),
        new Course("Estonian language level A2", 2, 65)
      ]
    };
  },
  methods: {},
  components: {
    Courses,
    Profile,
    Header,
    Footer
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  font-family: "Livvic", sans-serif;
}

html,
body {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100%;
  background-color: #eaeaea;
}

main {
  position: relative;
  min-height: 100%;
  padding-bottom: 110px;
}

#container {
  width: 80%;
  max-width: 900px;
  min-width: 320px;
  padding: 15px;
  background-color: #ffffff;
  margin: 0 auto;
}

.content {
  padding: 10px;
  border: 1px solid #cbcbcb;
  margin-bottom: 10px;
}

.tabs a {
  border: 1px solid #cbcbcb;
  background-color: #eaeaea;
  padding: 10px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  border-top: none;
  margin-top: -1px;
  outline: none !important;
}

.tabs a.active {
  background-color: #ffffff;
  border-top: 1px solid #ffffff;
}

.tabs a:hover {
  cursor: pointer;
}
</style>
