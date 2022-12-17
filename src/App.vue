<template>
  
    <v-toolbar height="100" dark>
      <v-spacer></v-spacer>
      <h1 class="text">TODO LISTs</h1>
      <v-spacer></v-spacer>
    </v-toolbar>
 
  <add-input></add-input>
</template>

<script>
import AddInput from "./components/AddInput.vue";
export default {
  components: {
    AddInput,
  },
};
</script>

<style>
body {
  min-height: 100vh;
  background-image: linear-gradient(rgb(191, 0, 255), pink, whiteSmoke);
}



.text {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}
</style>
