<template>
    <nav class="">
        <ul>
            <li 
               v-for="(item, index) in menu" :key="index"
               @click="MenuClick(item)" 
               >
               <a href="item.url">
                 {{item.name}}
               </a>
            </li>
        </ul>
    </nav>
</template>



<script>
export default {
    data(){
        return {
            menu: []
        };
    },
    async mounted() {
        const respons = await fetch('/menu.json');
        this.menu = (await respons.json()).menu;
        //console.log(this.menu);
    },
    methods: {
        MenuClick(clickitem){
         console.log('Вы кликнули на:', clickitem.name);
    },
}
}
</script>
<style scoped>
ul {
  list-style: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>