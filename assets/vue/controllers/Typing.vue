<template>
    <div>
      <input type="text" v-model="text" placeholder="Ecrivez quelque chose...">
       <p v-if="isTyping">Yanis est en train d'écrire...</p>
    </div>
  </template>
  
  <script setup>
  import {ref, watchEffect} from 'vue';
       const text = ref('');
       const isTyping = ref(false);
        const showTyping = () => {
            setTimeout(() => {
                isTyping.value = false;
            }, 3000)
        }

     const stopNow = watchEffect((onInvalidate) => {
          if(text.value.length > 0) {
              isTyping.value = true
              showTyping();

              if(text.value.length > 20) {
                stopNow();
              }

              onInvalidate(() => {
                  clearTimeout(showTyping)
              })
          }
      });

  </script>