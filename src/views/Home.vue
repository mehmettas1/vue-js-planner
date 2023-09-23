<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current"></FilterNav>
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.index">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import FilterNav from "@/components/FilterNav.vue";
import SingleProject from "@/components/SingleProject.vue";

// @ is an alias to /src

export default {
  name: "Home",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleComplete(id) {
      let p = this.project.find((project) => project.id === id);
      p.complete == !p.complete;
    },
  },

  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
};
</script>
