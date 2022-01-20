<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue';

export default {
  name: 'Home',
  components: {
    SingleProject,
  },
  data() {
    return {
      projects: [],
    };
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleComplete(id) {
      // this.projects = this.projects.map((project) => {
      //   if (project.id === id) {
      //     const updatedProject = { ...project, complete: !project.complete };
      //     return updatedProject;
      //   }
      //   return project;
      // });
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
