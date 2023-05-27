<template>
    <div>Hello {{ name }}!</div>
    <h2>{{ reactive }}</h2>

    <p>Ecrivez un message </p>
    <Typing />
    <button @click="click">Changer de variable</button>


    <div v-for="post in posts" :key="post.id">
        <p>Article {{ post.id }}</p>
        <p>Titre : {{ post.title }}</p>
        <p>Contenu: {{ post.body }}</p>
    </div>

    <p v-if="loading">Chargement en cours</p>


</template>

<script setup>
import Typing from './Typing.vue'
import {ref, onMounted, watchEffect} from 'vue'
const loading = ref(false)
const posts = ref([])



watchEffect(() => {

})

const loadPost =  () => {
    console.log("fecth post begin ");
    loading.value = true
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(res => {
        setTimeout(() => {
             posts.value = res
             loading.value = false
        }, 2000)
      } )


}
const reactive = ref("ceci est une variable reactive");
const click = () => {
    reactive.value = "La variable à bien étét modifié !"
}
onMounted(() => {
    loadPost()
})
defineProps({
        name: String  
    });


    
  
</script>