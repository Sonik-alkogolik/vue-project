<template>
    <div class="row">
     <div class="wrapper">
        <div
            class="row-item"
            v-for="photoItem in postitemsphotos" 
            :key="photoItem.id" 
            >
            {{ photoItem.message}}
            </div>
     </div>
 
     <div class="res_click_post">
    
     </div>
   </div>
   </template>
   
   <script>
   export default {
     data() {
       return {
        postitemsphotos: {},
        result_click: '',
       };
     },
     async mounted() {
       await this.requestApi();
    },
     methods: {
         async requestApi(){
             const response = await fetch('https://api.slingacademy.com/v1/sample-data/photos');
             this.postitemsphotos = await response.json();
            //  this.postitemsphotos = this.postitemsphotos.slice(0, 15); 
              console.log(this.postitemsphotos);
         },
        //  click_title(message,photos) {
        //     //  this.result_click = `ID${post.id} - Title${post.title}`;
        //  }
     },
   };
   </script>