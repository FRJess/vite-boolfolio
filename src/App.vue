<script>
import axios from 'axios';

export default {
    name: 'App',
    data(){
        return {
            baseUrl: 'http://127.0.0.1:8000/api/',
            projects : [],
            contentMaxLenght: 150,
            pagination:{
                current: 1,
                last: null
            }
        }
    },

    methods:{
        getApi(){
            axios.get(this.baseUrl + 'projects', {
                params:{
                    page: this.pagination.current
                }
            })
                .then(result => {
                    this.projects = result.data.projects.data;
                    console.log(this.projects)
                    this.pagination.current = result.data.projects.current_page;
                    this.pagination.last = result.data.projects.last_page;
                })
        },
        truncateText(summary){
            if(summary.length > this.contentMaxLenght){
                return summary.substr(0, this.contentMaxLenght) + '...';
            }
            return summary;
        }
    },
    mounted(){
        this.getApi(1);
    }
}

</script>

<template>

<div class="container">
  <h1>Projects list</h1>

  <div>
    <div v-for="project in projects" :key="project.name" class="project-box">
      <h3>{{project.name}}</h3>
      <p v-html="truncateText(project.summary)"></p>
    </div> 
  </div>

</div>

</template>

<style lang="scss">

@use './styles/general.scss';

</style>
