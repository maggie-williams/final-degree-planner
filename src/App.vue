<template>
  <div id="app" class="d-flex flex-column min-vh-100">
    <!-- Main Content -->
    <main class="flex-fill">
      <div class="container-fluid">
        <div class="row mb-5">
          <h1>Degree Planner</h1>
        </div>
        <div class="row main-content">
          <!-- Classes -->
          <div class="col-lg-4 required-classes">
            <h3>Required Classes</h3>

            <b-tabs content-class="mt-3">
              <!-- LAC Requirements -->

              <b-tab title="LAC" active>
                <div id="lac">
                  <div class="my-4 text-left" id="lac-reqs">
                    <CourseInfoCard 
                      v-for="c in lacCourses"
                      :course="c"
                      :key="c['Course ID']"
                      :options="options"
                      v-model="courseToAdd"
                    />
                  </div>
                </div>
              </b-tab>

              <b-tab title="CSIS">
                <div id="csis">
                  <div class="my-4 text-left" id="csis-reqs">
                    <CourseInfoCard 
                      v-for="c in csisCourses"
                      :course="c"
                      :key="c['Course ID']"
                      :options="options"
                      v-model="courseToAdd"
                    />
                  </div>
                </div>
              </b-tab>
              <b-tab title="CSSD">
                <div id="cssd">
                  <div class="my-4 text-left" id="cssd-reqs">
                    <CourseInfoCard 
                      v-for="c in cssdCourses"
                      :course="c"
                      :key="c['Course ID']"
                      :options="options"
                      v-model="courseToAdd"
                    />
                  </div>
                </div>
              </b-tab>
              <b-tab title="CYB">
                <div id="cyb">
                  <div class="my-4 text-left" id="cyb-reqs">
                    <CourseInfoCard 
                      v-for="c in cybCourses"
                      :course="c"
                      :key="c['Course ID']"
                      :options="options"
                      v-model="courseToAdd"
                    />
                  </div>
                </div>
              </b-tab>
              <b-tab title="IDD">
                <div id="idd">
                  <div class="my-4 text-left" id="idd-reqs">
                    <CourseInfoCard 
                      v-for="c in csisCourses"
                      :course="c"
                      :key="c['Course ID']"
                      :options="options"
                      v-model="courseToAdd"
                    />
                  </div>
                </div>
              </b-tab>

            </b-tabs>
          </div>

          <!-- Semester Schedules -->
          <div class="col-lg-6 semester-schedules">
            <h3>Semester Schedules</h3>

            <SemesterSchedule
              v-for="schedule in schedules"
              :schedule="schedule"
              v-bind:key="schedule.id"
            />
          </div>

          <div class="container">
            <div class="row">
              <div class="col-md-3">
                <img class="height-fix-chara-gumi" src="./assets/hero_chara_gumi.png" />
              </div>
              <div class="col-md-3">
                <img class="width-fix-chara-miku" src="./assets/hero_chara_miku.png" />
              </div>
            </div>
          </div>

          <!-- Table of Contents Sidebar -->
          <div class="col-lg-2 position-sticky top-0 h-100 ps-5 toc">
            <nav>
              <p class="text-muted">On this page</p>
              <ul>
                <li><a href="#fall2018">Fall 2018</a></li>
                <li><a href="#spring2019">Spring 2019</a></li>
                <li><a href="#fall2019">Fall 2019</a></li>
                <li><a href="#spring2020">Spring 2020</a></li>
                <li><a href="#fall2020">Fall 2020</a></li>
                <li><a href="#spring2021">Spring 2021</a></li>
                <li><a href="#fall2021">Fall 2021</a></li>
                <li><a href="#spring2022">Spring 2022</a></li>
              </ul>
            </nav>
          </div>
        </div>
      </div>
    </main>

    <!-- Footer -->
    <footer class="bg-dark text-light py-4">
      <div class="container-fluid">
        <div class="row">
          <div class="col">
            <p>Made with ❤️ by FHU students!</p>
          </div>

          <div class="col-md-3">
            <p>&copy; 2021 Freed-Hardeman University</p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import CourseInfoCard from './components/CourseInfoCard.vue'
import SemesterSchedule from './components/SemesterSchedule.vue'
import lacCoursesFromFile from './lac.json'
import csisCoursesFromFile from './csis.json'
import cssdCoursesFromFile from './cssd.json'
import iddCoursesFromFile from './idd.json'
import cybCoursesFromFile from './cyb.json'

export default {
  name: "App",
  components: {
    CourseInfoCard,
    SemesterSchedule
  },
  watch: {
    courseToAdd(courseCard) {
      const index = this.schedules.findIndex(s => s.id == courseCard.semester);
      this.schedules[index].classes.push(courseCard.course);
    }
  },
  data() {
    return {
      courseToAdd: null,
      schedules: [
        {
          name: "Fall 2018",
          id: "fall2018",
          season: "fall",
          collapseId: "fall2018schedule",
          classes: [],
        },
        {
          name: "Spring 2019",
          id: "spring2019",
          season: "spring",
          collapseId: "spring2019schedule",
          classes: [],
        },
        {
          name: "Fall 2019",
          id: "fall2019",
          season: "fall",
          collapseId: "fall2019schedule",
          classes: [],
        },{
          name: "Spring 2020",
          id: "spring2020",
          season: "spring",
          collapseId: "spring2020schedule",
          classes: [],
        },{
          name: "Fall 2020",
          id: "fall2020",
          season: "fall",
          collapseId: "fall2020schedule",
          classes: [],
        },{
          name: "Spring 2021",
          id: "spring2021",
          season: "spring",
          collapseId: "spring2021schedule",
          classes: [],
        },{
          name: "Fall 2021",
          id: "fall2021",
          season: "fall",
          collapseId: "fall2021schedule",
          classes: [],
        },{
          name: "Spring 2022",
          id: "spring2022",
          season: "spring",
          collapseId: "spring2022schedule",
          classes: [],
        },
      ],

      lacCourses: lacCoursesFromFile,
      cybCourses: cybCoursesFromFile,
      csisCourses: csisCoursesFromFile,
      cssdCourses: cssdCoursesFromFile,
      iddCourses: iddCoursesFromFile,

      options: [
        { value: "fall2018", text: "Fall 2018" },
        { value: "spring2019", text: "Spring 2019" },
        { value: "fall2019", text: "Fall 2019" },
        { value: "spring2020", text: "Spring 2020" },
        { value: "fall2020", text: "Fall 2020" },
        { value: "spring2021", text: "Spring 2021" },
        { value: "fall2021", text: "Fall 2021" },
        { value: "spring2022", text: "Spring 2022" },
      ],
      selected: null,
    };
  },
  methods: {
    addCourseToSchedule(value) {
      console.log(value);
    }
  },
};
</script>

<style>
#app {
  font-family: "Nunito Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.toc nav {
  text-align: left;
}

.toc ul {
  padding: 0;
  list-style: none;
}

.toc li {
  margin: 0;
  margin-bottom: 0.5rem;
}

.toc li a {
  text-decoration: none;
}

.toc li a:hover {
  text-decoration: underline;
}

.required-classes .card {
  border-left: 8px solid #0c63e4;
}

.full-width {
  width: 100%;
}

.height-fix-chara-gumi {
  max-height: 449px;
}

.width-fix-chara-miku{
  max-width: 330px;
}
</style>
