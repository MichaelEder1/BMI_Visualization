<template>
    <!-- assumption: we will get the petName from a form and pass it together with the already calculated bmi to this component -->
  <BmiVisualization petName="Luna" bmiValue="89.28"/>
</template>

<script>
import BmiVisualization from "@/components/BmiVisualization.vue";

export default {
  name: 'App',
  components: {
    BmiVisualization,
  }
}
</script>

<style>
:root {
  --main-color: #007fC8;
  --grey: #BFBFBF;
  --red: #F25E5A;
  --green: #35F275;
}
#app {
  font-family: 'Roboto', 'Montserrat', 'Lato', sans-serif;
  text-align: center;
  font-size: 1rem;
}
</style>
