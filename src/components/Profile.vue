<template>
  <div id="profile">
    <div class="avatar">
      <img src="../assets/me.png" id="picture" alt="My picture" />
    </div>
    <div class="info">
      <ul>
        <li id="name">{{user.firstname + " " + user.lastname}}</li>
        <li id="birthdate">{{user.birthdate}}</li>
        <li id="faculty">{{user.faculty}}</li>
      </ul>
    </div>
    <div id="gpa">
      <strong>{{this.calculateAverage}}</strong>
    </div>
    <div class="clear-fix"></div>
  </div>
</template>

<script>
import User from "../User.js";

export default {
  name: "Profile",
  data: () => {
    return {
      user: new User("John", "Doe", "11/10/1990", "Software Engineering", 2.75)
    };
  },
  methods: {
    //funktsioon, mis arvutab 0-4-ni hinde väärtuse, mis on antud algul 0-100 väärtusena
    GPA: function(avgGra) {
      if (avgGra > 90) {
        return 4;
      } else if (avgGra > 80) {
        return 3;
      } else if (avgGra > 70) {
        return 2;
      } else if (avgGra > 60) {
        return 1;
      } else if (avgGra > 50) {
        return 0.5;
      } else {
        return 0;
      }
    }
  },
  computed: {
    //keskmise arvutamise funktsioon.
    calculateAverage: function() {
      let summa = 0;
      for (let i = 0; i < this.allCourses.length; i++) {
        //oluline on, et kasutatud parseInt-i muidu jätab stringiks pärast arvutades.
        summa += parseInt(this.GPA(this.allCourses[i].grade));
      }
      summa = summa / this.allCourses.length;
      return summa.toFixed(2);
    }
  },
  props: {
    allCourses: Array
  }
};
</script>

<style scoped>
#profile {
  border-bottom: 1px dashed #a7a7a7;
  padding-bottom: 10px;
  margin-bottom: 10px;
}

#profile div:not(.clear-fix) {
  height: 190px;
  float: left;
  position: relative;
}
.clear-fix {
  clear: both;
}

#profile .avatar {
  width: 35%;
  text-align: center;
}

#profile .avatar img {
  width: 180px;
}

#profile .info {
  width: 45%;
}

#profile #gpa {
  width: 20%;
}

#profile #gpa strong {
  position: absolute;
  width: 100%;
  height: 60px;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto auto;
  font-size: 60px;
  line-height: 60px;
  text-align: center;
}
</style>