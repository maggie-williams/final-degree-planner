<template>
  <div class="accordion my-4" :id="schedule.id">
    <div class="accordion-item">
      <h2
        class="accordion-header"
        :id="`${schedule.id}heading`"
        v-b-toggle:[schedule.collapseId]
      >
        <div class="">
          <h4 class="my-0">{{ schedule.name }}</h4>
        </div>
      </h2>
      <b-collapse :id="schedule.collapseId">
        <div class="accordion-body">
          <table class="table table-hover">
            <thead>
              <th>Course</th>
              <td></td>
              <td></td>
              <th>Credits</th>
              <td></td>
            </thead>
            <tr v-for="course, index in schedule.classes" :key="index">
              <td>{{course["Course ID"]}}</td>
              <td>
                <span class="fw-bold">{{course["Course Name"]}}</span>
              </td>
              <td>
                <span class="badge bg-primary">{{course["Category"]}}</span>
              </td>
              <td>{{course["Credit Hours"]}}</td>
              <td>
                <img 
                  @click="removeCourse(index)"
                  width="32"
                  src="../assets/trash.png"
                />
              </td>
            </tr>
            <tr>
              <td></td>
              <td></td>
              <td></td>
              <td class="fw-bold">{{ creditHours }}</td>
            </tr>
          </table>
        </div>
      </b-collapse>
    </div>
  </div>
</template>

<script>
export default {
  name: "SemesterSchedule",
  props: {
    schedule: Object
  },
  created() {
  },
  methods: {
    removeCourse(index) {
      this.schedule.classes.splice(index, 1);
    }
  },
  computed: {
    creditHours() {
      let count = 0;
      this.schedule.classes.forEach(c => {
        count += +c["Credit Hours"]
      });
      return count;
    }
  }
};
</script>
