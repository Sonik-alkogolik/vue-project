<template>
    <div>
        <div v-for="post in postitems" :key="post.id">
            <h3>{{ post.title }}</h3>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        postitems: []
      };
    },
    async mounted() {
      await this.requestApi();
   },
    methods: {
        async requestApi(){
            const response = await fetch('https://jsonplaceholder.typicode.com/posts');
            this.postitems = await response.json();
            console.log(this.postitems);
            
        },
    },
  };
  </script>
  