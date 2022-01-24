<template>
  <div class="home">
    <FilterNav @onFilter="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue';
import FilterNav from '../components/FilterNav.vue';

export default {
  name: 'Home',
  components: {
    SingleProject,
    FilterNav,
  },
  data() {
    return {
      projects: [],
      current: 'all',
    };
  },
  computed: {
    filteredProjects() {
      switch (this.current) {
        case 'completed':
          return this.projects.filter((project) => project.complete);
        case 'ongoing':
          return this.projects.filter((project) => !project.complete);
        default:
          return this.projects;
      }
    },
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleComplete(id) {
      const p = this.projects.find((project) => project.id === id);
      p.complete = !p.complete;
    },
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then((res) => res.json())
      .then((data) => {
        this.projects = data;
      })
      .catch((e) => console.log(e.message));
  },
};
</script>

<style lang="scss" scoped></style>
