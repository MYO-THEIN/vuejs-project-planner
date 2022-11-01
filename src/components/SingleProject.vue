<template>
    <div class="project" :class="{complete: project.complete}">
        <div class="flexing">
            <div>
                <h3 @click="showDetail = !showDetail">{{project.title}}</h3>
            </div>
            <div>
                <span class="material-icons" @click="completeProject">done</span>
                <router-link :to="{name:'editProject', params:{id: project.id} }">
                    <span class="material-icons">edit</span>
                </router-link>
                <span class="material-icons" @click="deleteProject">delete</span>
            </div>
        </div>
        <p v-if="showDetail">{{project.detail}}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            api: "http://localhost:3000/projects/",
            showDetail: false
        }
    },
    methods: {
        completeProject() {
            fetch(this.api + this.project.id, {
                method: "PATCH",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({
                    complete: !this.project.complete
                })
            })
            .then(()=>{
                this.$emit("completedProject", this.project.id);
            })
            .catch((error)=>{
                console.log(error.message);
            });
        },
        deleteProject() {
            fetch(this.api + this.project.id, {method: "DELETE"})
            .then(()=>{
                this.$emit("deletedProject", this.project.id);
            })
            .catch((error)=> {
                console.log(error.message);
            });
        }
    },
    props: [
        'project'
    ]
}
</script>

<style>
.flexing {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.project {
    background-color: #F2F2F2;
    padding: 20px;
    margin: 10px;
    border-left: 5px solid crimson;
    border-radius: 10px;
}
.complete {
    border-left-color: green;
}
h3 {
    color: indigo;
    cursor: pointer; 
}
span {
    margin-left: 3px;
    cursor: pointer;
}
span:hover {
    color: grey;
}
</style>
