<template>
  <form @submit.prevent="handleSubmit">
    <label>Title:</label>
    <input type="text" v-model="title" required/>
    <label>Details:</label>
    <textarea v-model="details"></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  name: "EditProjectView",
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      uri: 'http://localhost:3000/projects/' + this.id
    };
  },
  mounted() {
    fetch(this.uri)
        .then(res => res.json())
        .then(data => {
          this.title = data.title
          this.details = data.details
        })
  },
  methods: {
    handleSubmit() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: {'Content-Type': 'Application/json'},
        body: JSON.stringify({title: this.title, details: this.details})
      }).then(() => {
        this.$router.push('/')
      }).catch(err => console.log(err.message))
    }
  }
};
</script>

<style scoped>
form {
  background-color: #fff;
  padding: 20px;
  border-radius: 3px;
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

input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}

textarea {
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
}

form button {
  display: block;
  margin: 20px auto 0;
  background-color: #42b983;
  color: #fff;
  padding: 10px;
  border: 0;
  border-radius: 3px;
  font-size: 14px;
}
</style>