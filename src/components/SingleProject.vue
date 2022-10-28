<template>
    <div class="project">
        <div class="flexing">
            <div>
                <h3 @click="showDetail = !showDetail">{{project.title}}</h3>
            </div>
            <div>
                <span class="material-icons">done</span>
                <span class="material-icons">edit</span>
                <span class="material-icons">delete</span>
            </div>
        </div>
        <p v-if="showDetail">{{project.detail}}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            showDetail: false
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
h3 {
    color: indigo;
    cursor: pointer; 
}
span {
    margin-left: 3px;
}
span:hover {
    color: blue;
}
</style>
