<template>
   <v-app id="inspire"
     class="pa-10">
      <v-row justify="center">
    <v-card
        class="pa-10"
    height="450"
    width="500">
  <div>
   <p>FullName:{{kumud.name}}</p>
   <p>Email:{{kumud.email}}</p>
   <p>PhoneNo:{{kumud.phoneno}}</p>
   <p>State:{{kumud.state}}</p>
</div>
</v-card>
</v-row>
</v-app>
  </template>
  <script>
     export default {
    name: "FormInfo",
    
    props: [ 'kumud']
    
}
     
  </script>