<template>
  <h1>Add a new project</h1>
  <form @submit.prevent="addProject">
    <label>Project Title</label>
    <input type="text" v-model="title" />
    <label>Project Detail</label>
    <input type="text" v-model="detail" />
    <button>Save</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      api: "http://localhost:3000/projects/",
      detail: null,
      title: null,
    }
  },
  methods: {
    addProject() {
      fetch(this.api, {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          "title": this.title,
          "detail": this.detail,
          "complete": false
        })
      })
      .then(()=>{
        this.$router.push({name: 'home'});
      })
      .catch((error)=>{
        console.log(error.message);
      });
    }
  }
}
</script>

<style>
form {
  background-color: white;
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
  margin: 20px 0 10px 0
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
  background-color: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
}
</style>
