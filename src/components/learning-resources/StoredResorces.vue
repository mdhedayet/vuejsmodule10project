<template>
  <ul>
      <learning-resources v-for="res in resorces" :key="res.id"
      :title="res.title"
      :description="res.description"
      :link="res.link"
      ></learning-resources>
  </ul>
</template>

<script>
import LearningResources from './LearningResource.vue'
export default {
    components: {
        LearningResources,
        },
inject:['resorces']
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}

</style>