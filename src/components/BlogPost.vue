<template>
   <div class="row">
    <div class="wrapper">
        <div
        class="row-item"
        v-for="post in postitems" 
        :key="post.id"
        @click="click_title(post)"
        >
            <h3>{{ post.title }}</h3>
              <p>{{ post.id}}</p>
        </div>
    </div>

    <div class="res_click">
      Клик по: {{ result_click }}
    </div>
  </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        postitems: [],
        result_click: '',
      };
    },
    async mounted() {
      await this.requestApi();
   },
    methods: {
        async requestApi(){
            const response = await fetch('https://jsonplaceholder.typicode.com/posts');
            this.postitems = await response.json();
            this.postitems = this.postitems.slice(0, 15); 
            //  console.log(this.postitems);
        },
        click_title(post) {
            this.result_click = `ID${post.id} - Title${post.title}`;
        }
    },
  };
  </script>
  
  <style>
.wrapper {
  display: flex;
  flex-direction: column;
}
.row {
  display: flex;
}
  .row-item {
    display: flex;
    align-items: center;
  }
  .res_click {
    max-width: 300px;
    width: 100%;
    font-size: 14px;
  }
</style>