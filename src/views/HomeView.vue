<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current"/>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
      <singleProject :project="project" @delete="handleDelete" @complete="handleComplete"/> 
        
      </div>
    </div>
  </div>
</template>

<script>
import FilterNav from "../components/FilterNav.vue";
import singleProject from "../components/singleProject.vue";
export default {
  name: 'HomeView',
  components:{singleProject , FilterNav},
  data(){
    return{
      projects: [],
      current: "all"
    }
  },
  mounted(){
    fetch("  http://localhost:3000/projects")
    .then(res => res.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id){
      this.projects = this.projects.filter(item =>{
        return item.id !== id;
      })
    },
    handleComplete(id){
       let p = this.projects.find(item => {
        return item.id === id
       })
       console.log(p.complete);
      p.complete = !p.complete;
    }
  },
  computed:{
    filteredProjects(){
      if(this.current === 'completed'){
        return this.projects.filter(item => item.complete)
      }
      else if(this.current === 'ongoing'){
        return this.projects.filter(item => !item.complete)
      }
      else{
        return this.projects
      }
    }
  }

}
</script>
