<script>
export default {
  name: 'ProjectCards',

  props: {
    project: Object,
  },

  data() {
    return {};
  },

  mounted() {},

  methods: {}
}
</script>

<template>
  <div class="card">
    <div class="card-body">
      <h2 class="card-title">{{ project.title }}</h2>
      <p class="card-text">{{ project.description }}</p>

    </div>
    <img class="card-img-top mt-2" :src="'/images/' + project.image" alt="Copertina">
    
  </div>
</template>

<style lang="scss"></style>
