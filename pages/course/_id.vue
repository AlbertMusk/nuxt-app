<template>
  <div class="pa-3">
    <v-btn to="/source" text>返回</v-btn>
    <h3 class="mt-3">{{course.name}}</h3>
    <v-select
      v-model="currentIndex"
      :items="course.episodes.map((v, i) => ({text: v.name, value: i}))"></v-select>
    <img :src="course['coverUrl']" alt="">
  </div>
</template>

<script>
  export default {
    data() {
      return {
        id: '',
        course: {},
        currentIndex: 0
      }
    },
    async asyncData({$axios, params}) {
      const ret = await $axios.$get(`/course/${params.id}`);
      return {
        course: ret['data']
      }
    }
  }
</script>

<style scoped>

</style>
