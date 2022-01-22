<template>
  <form @submit.prevent="handleSubmit">
    <label for="title">Title: </label>
    <input type="text" id="title" required v-model="title" />
    <label for="details">Details</label>
    <textarea id="details" required v-model="details"></textarea>
    <button>Add Project</button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      title: '',
      details: '',
    };
  },
  methods: {
    handleSubmit() {
      console.log(this.title, this.details);
    },
  },
};
</script>
<style lang="scss" scoped>
form {
  background: white;
  padding: 20px;
  border-radius: 10px;
}
label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input,
textarea {
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
}
input {
  border: 0;
  border-bottom: 1px solid #ddd;
}
textarea {
  border: 1px solid #ddd;
  padding: 10px;
  height: 100px;
}
form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>
