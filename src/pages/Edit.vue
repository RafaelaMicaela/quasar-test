<template>
  <q-page class="q-pa-lg">

    <h5 class="q-mt-none">Edit Info</h5>
      <q-input 
      outlined 
      v-model="name" 
      label="name"
      class="q-mb-md" 
      />
      <q-input 
      outlined 
      v-model="username" 
      label="username" 
      />
      <q-btn 
      class="q-mt-md"
      color="primary" 
      label="Edit" 
      />
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default {
  
  data(){
    return{
      name: '',
      username: ''
    }
  }
}
</script>
