<template>
<FilterNav @filterChange="sentBtnValue($event)" :current="current"/>
  <div v-if="projects.length">
    <div v-for="project in filteredProjects" :key="project.id">
      <SingleProject
        :project="project"
        @delete="handleDelete"
        @complet="handleComplete"
      />
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue"

export default {
  name: "HomeView",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: 'all'
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((resp) => resp.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => project.id != id);
    },
    handleComplete(id){
      let p = this.projects.find(project => {
        return project.id === id
        });
      p.complete = !p.complete
    },
    sentBtnValue(e){
      console.log('Heyyy', e)
      this.current = e;
    }
  },
  computed: {
    filteredProjects(){
      if(this.current === 'completed'){
        return this.projects.filter(project => project.complete);
      }
      if(this.current === 'ongoing'){
        return this.projects.filter(project => !project.complete);
      }
      return this.projects;
    }
  }
};
</script>
