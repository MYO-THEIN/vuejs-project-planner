<template>
  <div class="home">
    <h1>Home</h1>
    <FilterNav @filterValue="current=$event" :current="current" />
    <div v-for="project in filteredProjects" :key="project.id">
      <SingleProject :project="project" comple
        @completedProject="completedProject"
        @deletedProject="deletedProject" />
    </div>
  </div>
</template>

<script>
import FilterNav from '../components/FilterNav.vue';
import SingleProject from '../components/SingleProject.vue';

export default {
  name: 'HomeView',
  components: {
    FilterNav,
    SingleProject
  },
  computed: {
    filteredProjects() {
      if (this.current === 'complete')
        return this.projects.filter((p)=>{
          return p.complete;
        });
      else if (this.current === 'ongoing')
        return this.projects.filter((p)=>{
          return !p.complete;
        });
      else
        return this.projects;
    }
  },
  data() {
    return {
      current: "all",
      projects: []
    }
  },
  methods: {
    completedProject(id) {
      let prj = this.projects.find((proj)=>{
        return proj.id === id;
      });
      prj.complete = !prj.complete;
    },
    deletedProject(id) {
      this.projects = this.projects.filter((proj)=>{
        return proj.id !== id;
      });
    }
  },
  mounted() {
    fetch("http://localhost:3000/projects")
    .then((response)=>{
      return response.json();
    })
    .then((data)=>{
      this.projects = data;
    })
    .catch((error)=>{
      console.log(error.message);    
    });
  }
}
</script>

<style scoped>

</style>
