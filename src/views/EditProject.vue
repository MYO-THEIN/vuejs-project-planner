<template>
  <h1>Edit project</h1>
  <form @submit.prevent="editProject">
    <label>Project Title</label>
    <input type="text" v-model="title" />
    <label>Project Detail</label>
    <input type="text" v-model="detail" />
    <button>Update</button>
  </form>
</template>

<script>
export default {
    props: [
        'id'
    ],
    data() {
        return {
            api: "http://localhost:3000/projects/",
            detail: "",
            title: ""
        }
    },
    methods: {
        editProject() {
            fetch(this.api + this.id, {
                method: "PATCH",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({
                    "title": this.title,
                    "detail": this.detail
                })
            })
            .then(()=>{
                this.$router.push({name: 'home'});
            })
            .catch((error)=>{
                console.log(error.message);
            })
        }
    },
    mounted() {
        fetch(this.api + this.id)
        .then((response)=>{
            return response.json();
        })
        .then((data)=>{
            this.title = data.title;
            this.detail = data.detail;
        })
        .catch((error)=>{
            console.log(error.message);
        })
    }
}
</script>

<style>

</style>
