<template>
  <div class="project" :class="{complete: project.complete}">
    <div class="actions"> 
        <h3 @click="showDetail = !showDetail">{{project.title}}</h3>
        <div class="icons">
            <router-link :to="{name: 'EditProject' , params: {id: project.id}}">
            <i class="fa-solid fa-pen icon"></i>
            </router-link>
            <i @click="deleteProject" class="fa-solid fa-trash icon"></i>
            <i @click="changeComplete" class="fa-solid fa-check icon"></i>
        </div>
    </div>
    <div v-if="showDetail" class="detail">
        <p>{{project.details}}</p>
    </div>
    
  </div>
</template>

<script>
export default {
    props:["project"],
    data(){
        return{
            showDetail: false,
            url: "http://localhost:3000/projects/" + this.project.id
        }
    },
    methods:{
        deleteProject(){
            fetch(this.url, {
                method: 'DELETE'
            })
            .then(()=> this.$emit('delete' , this.project.id))
            .catch(err => console.log(err.message))
            
        },
        changeComplete(){
            fetch(this.url, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json'},
                body: JSON.stringify({complete: !this.project.complete})
            })
            .then(()=> this.$emit('complete', this.project.id))
            .catch(err => console.log(err.message))
        }
    }
}
</script>

<style>
.project{
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);
    border-right: 4px solid #e90074;
}
.project.complete{
    border-right: 4px solid #00ce89 ;
}
h3{
    cursor: pointer;
}
.icon{
    margin: 0 5px;
    color: #bbb;
    cursor: pointer;
}
.icon:hover{
    color: #777;
}
.actions{
    display: flex;
    justify-content: space-between;
    align-items: center;
}

</style>