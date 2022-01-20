<template>
  <div class="project">
    <div class="project__actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <span class="material-icons"> edit </span>
        <span class="material-icons"> delete </span>
        <span class="material-icons"> done </span>
      </div>
    </div>
    <div v-if="showDetails" class="project__details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      showDetails: false,
    };
  },
  props: {
    project: Object,
  },
};
</script>
<style lang="scss" scoped>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
  h3 {
    cursor: pointer;
  }
  &__actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .material-icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
  }
  .material-icons:hover {
    color: #777;
  }
}
</style>
