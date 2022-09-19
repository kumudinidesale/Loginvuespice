<template>
  
    <v-main>
      
    <div class="text-center">
      <v-btn
        rounded
        color="white"
        dark
        @click="showForm"
      >
         Button1
      </v-btn>
      <v-btn
        rounded
        color="white"
        dark
        @click="showInfo" 
      >
        Button2
      </v-btn>
      </div>
      
      <FillTheForm @input="datar" v-if="showTheData"/>
      <FormInfo :kumud="FillData" v-if="showpage"/>
    </v-main>
  
</template>

<script>
  

import FillTheForm from './components/FillTheForm.vue';
import FormInfo from './components/FormInfo.vue';

export default {
  name: 'App',

  components: {
   
    FillTheForm,
    FormInfo
},

  data(){
    return{
      FillData:{},
      showTheData:false,
      showpage:false,

    }
  },
  methods:{
    datar(payload){
      console.log(payload);
      this.FillData=payload;
      this.showTheData=false;
      this.showpage=true;
      
    },
    showForm(){
      this.showTheData=true;
      this.showpage=false;
    },
    showInfo(){
      this.showTheData=false;
      this.showpage=true;
    }
  }
};
</script>
