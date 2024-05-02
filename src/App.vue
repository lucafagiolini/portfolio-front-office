<script>
import axios from 'axios';

export default {
  data() {

    return {
      projects: [],
      baseApiUrl: 'http://127.0.0.1:8000/api',
      apilinks: [],
      apiPage: 1,
  


    }

  },

  mounted() {
    this.apiCall();
  },

  methods: {
    apiCall() {
      axios.get(this.baseApiUrl + '/projects', {
      params: {
        page: this.apiPageNumber,
      }
    }) 
      .then(response => {
        this.projects = response.data.results;

        this.apilinks = response.data.results.links;

      })

    },
    changeApiPage(pageNumber) {
      this.apiPageNumber = pageNumber;
      this.apiCall();
      
    }

    

  },
  
}

</script>

<template>

  <div class="container">

    <div>
      <h1 class="pt-5">Projects:</h1>
      <hr>
      <ul class="d-flex justify-content-center flex-wrap gap-3 ">
        <li class="d-flex flex-column align-items-center" v-for="project in projects.data" :key="project.id">
          <h2>{{ project.title }}</h2>
          <p>{{ project.description }}</p>
          <p>{{ project.link}}</p>
        </li>
      </ul>
    </div>

    <hr>

    <nav class="pt-5">
      <ul class="d-flex justify-content-center gap-3">

        <li v-for="link in apilinks" v-html="link.label" @click="changeApiPage(link.label)" style="list-style: none;">
        </li>

      </ul>

    </nav>

  </div>

 
</template>

<style lang="scss" scoped>

li {

  
  padding: 8px;
  cursor: pointer;
  

  text-decoration: none;
  color: white;
  user-select: none;

  transition: all 0.3s ease-in-out;

  &:hover {
    background-color: #f8f9fa;
    color: black;
  }
}

</style>
