<template>
  <div class="card my-2">
    <div class="card-body">
      <div class="row">
        <h5 class="col-9">
          <b>{{ course["Course Name"] }}</b>
        </h5>
        <p class="col-3 text-right">{{course["Credit Hours"]}}</p>
      </div>

      <div class="row">
        <div class="col-8">
          <p class="card-subtitle">{{course["Course ID"]}}</p>
        </div>
        <div class="col-4 text-right">
          <span class="text-muted">{{course["Semester Offered"]}}</span>
        </div>
      </div>
      <div class="row">
        <b-form-select v-model="selected" :options="filteredOptions"></b-form-select>

        <b-button
          block
          variant="outline-secondary"
          class="my-2"
          @click="addCourse"
        >
          Add
        </b-button>
      </div>

      <div class="row">
        <div class="col">
          <a :href="`#${shortID}`" class="card-link fw-light" v-b-toggle:shortID
            >Course description ›</a
          >
        </div>
      </div>

      <b-collapse class="course-description collapse card-text" :id="shortID">
        <p class="text-muted card-text">
          {{course["Course Description"]}}
        </p>
      </b-collapse>
    </div>
  </div>
</template>

<script>
export default {
  name: "CourseInfoCard",
  props: {
    course: Object,
    options: Array,
  },
  data() {
    return {
      selected: null,
    }
  },
  methods: {
    convertID(courseID) {
      return courseID.replace(" ", "").replace("/", "-").toLowerCase();
    },
    addCourse() {
      this.$emit("input", {
        course: this.course,
        semester: this.selected
      });
    }
  },
  computed: {
    shortID() {
      return this.course['Course ID'].replace(" ", "").replace("/", "-").toLowerCase();
    },
    filteredOptions() {
      const validSeasons = this.course["Semester Offered"].replace(" -", ", ").split(", ");

      return this.options.filter(o => {
        const optSeason = o.text.split(" ")[0];
        return validSeasons.includes(optSeason);
      })
    },
  }
};
</script>

<style></style>
