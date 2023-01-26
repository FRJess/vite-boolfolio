<script>
export default {
  name: "ProjectCard",
  props:{
    project: Object,
  }
};
</script>

<template>

  <div class="card">

    <h3>{{project.name}}</h3>
    <h4 v-if="project.type">Type: {{ project.type.name }}</h4>
    <div class="technologies" v-if="project.technologies.length">
      <span v-for="technology in project.technologies" :key="technology.id">{{ technology.name }}</span>
    </div>
    <p v-html="(project.summary)"></p>

  </div>
  
</template>


<style lang="scss">

@use '../styles/general.scss';

</style>