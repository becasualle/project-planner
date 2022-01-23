<template>
  <form @submit.prevent="handleSubmit">
    <label for="title">Title: </label>
    <input type="text" id="title" required v-model="title" />
    <label for="details">Details</label>
    <textarea id="details" required v-model="details"></textarea>
    <button>Update Project</button>
  </form>
</template>
<script>
export default {
  props: {
    id: String,
  },
  data() {
    return {
      title: '',
      details: '',
      uri: `http://localhost:3000/projects/${this.id}`,
    };
  },
  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
      })
      .catch((e) => console.log(e));
  },
  methods: {
    handleSubmit() {
      const project = {
        title: this.title,
        details: this.details,
      };
      const options = {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project),
      };
      fetch(this.uri, options)
        .then(() => this.$router.push('/'))
        .catch((e) => console.log(e));
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
