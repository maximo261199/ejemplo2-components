<script setup>
import { onMounted, ref } from "vue";


import ButtonCounter from "./components/ButtonCounter.vue";
import BlogPost from "./components/BlogPost.vue";

import PaginatePost from "./components/PaginatePost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([])
const loading = ref(true); 

const favorito = ref("");
const postXpage = 10
const inicio = ref(0);
const fin = ref(postXpage);
const cambiarFavorito = (titulo) =>{
  favorito.value=titulo;
};

const next = () =>{
inicio.value = inicio.value+postXpage; 
fin.value = fin.value+postXpage;
}
const prev = () =>{
  if (inicio.value === 0){}
  else {
    inicio.value = inicio.value-postXpage; 
fin.value = fin.value-postXpage;  
  }

}
onMounted(async() =>{
   loading.value = true;
   try{
   const res = await fetch('https://jsonplaceholder.typicode.com/posts')
  posts.value = await res.json()  
  } catch(error){console.log(error)}
  finally {
    setTimeout(() => {
      loading.value =  false;
    }, 2000);
  }

})





</script>
/*
fetch('https://jsonplaceholder.typicode.com/posts')
.then((res) => res.json())
.then((data)=> {posts.value = data})
.catch((e) => console.log(e))
.finally(()=>{
  setTimeout(() => {      
    loading.value = false;
   }, 2000);
});

*/

// mb-2 margin button
/*
const masLength = computed(() => posts.value.length);
*/


<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container" v-else>
    <h1>App</h1>
    <h2>Mis posts favorito: {{favorito}}</h2>

    <PaginatePost class="mb-2"
    @cambioNext = "next"
    @cambioPrev = "prev"
    :inicio="inicio"
    :fin = "fin"
    :maxLength = "posts.length"

    ></PaginatePost>
  <BlogPost
  v-for="post in posts.slice(inicio,fin)" 
  :key="post.id"
  :title="post.title"
  :id="post.id"
  :body="post.body"
  @cambiarFavoritoNombre="cambiarFavorito"
  class="mb-2"
   

  > 
 
  </BlogPost>

//evento personalizado
   </div>

</template>