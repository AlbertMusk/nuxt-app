<template>
  <v-card>
    <v-tabs
      v-model="tab"
      background-color="primary"
      dark
    >
      <v-tab
        v-for="item in items"
        :key="item.tab"
        :to="`/cms/${item.tab}`"
      >
        {{ item.tab }}
      </v-tab>
    </v-tabs>


    <nuxt-child keep-alive></nuxt-child>
  </v-card>
</template>

<script>
  export default {
    name: "index",
    data() {
      return {
        tab: 0,
        items: [
          {tab: "course"},
          {tab: "episode"}
        ],
        data: []
      }
    }
  }
</script>

<style scoped>

</style>
