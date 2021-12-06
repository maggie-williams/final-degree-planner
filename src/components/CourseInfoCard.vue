<template>
  <div class="card my-2">
    <div class="card-body">
      <div class="row">
        <h5 class="col-9">
          <b>{{ course["Course Name"] }}</b>
        </h5>
        <p class="col-3 text-right">2 hours</p>
      </div>

      <div class="row">
        <div class="col-8">
          <p class="card-subtitle">BIB 121</p>
        </div>
        <div class="col-4 text-right">
          <span class="text-muted">Fall</span>
        </div>
      </div>
      <div class="row">
        <b-form-select v-model="selected" :options="options"></b-form-select>

        <b-button block variant="outline-secondary" class="my-2">Add</b-button>
      </div>

      <div class="row">
        <div class="col">
          <a href="#bib121" class="card-link fw-light" v-b-toggle:shortID
            >Course description ›</a
          >
        </div>
      </div>

      <b-collapse class="course-description collapse card-text" :id="shortID">
        <p class="text-muted card-text">
          A thorough textual study of the life of Jesus the Christ. Emphasis is
          given to his virgin birth, his message and ministry, his crucifixion,
          his resurrection, and his ascension, all leading to a greater
          awareness of his greatness as the Son of God and Savior of the world.
          Moral, doctrinal, historical, and practical aspects of the life of
          Christ are also emphasized. (Text course.)
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
  },
  methods: {
    convertID(courseID) {
      return courseID.replace(" ", "").replace("/", "-").toLowerCase();
    },
  },
  computed: {
    shortID() {
      return this.course['Course ID'].replace(" ", "").replace("/", "-").toLowerCase();
    }
  }
};
</script>

<style></style>
