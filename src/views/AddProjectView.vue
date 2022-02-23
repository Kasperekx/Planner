<template>
  <form @submit.prevent="handleSubmit">
    <label>Title:</label>
    <input type="text" v-model="title" required>
    <label>Details</label>
    <textarea v-model="details" required></textarea>
    <button>Add project</button>
  </form>
</template>

<script>
export default {
  name: "AddProjectView",
  data() {
    return {
      title: '',
      details: ''
    }
  },
  methods: {
    handleSubmit() {
      let project = {
        title: this.title,
        details: this.details,
        complete: false
      }
      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: {'Content-Type': 'Application/json'},
        body: JSON.stringify(project)
      }).then(() => {
        this.$router.push('/')
      }).catch(err => console.log(err.message))
    }
  }
}
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