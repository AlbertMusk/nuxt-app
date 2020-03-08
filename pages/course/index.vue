<template>
  <div class="pa-3">
    <h4>课程列表({{count}})</h4>

    <v-row>
      <v-col
        v-for="(course, index) in courses"
        :key="index">
        <v-card
          class="mx-auto"
          max-width="344"
          :to="`/course/${course._id}`"
        >
          <v-img
            :src="course['coverUrl']"
            height="200px"
          ></v-img>

          <v-card-title>
            {{course['name']}}
          </v-card-title>

          <v-card-subtitle>
            {{course['description']}}
          </v-card-subtitle>

          <v-card-actions>
            <v-btn text>Share</v-btn>

            <v-btn
              color="purple"
              text
            >
              Explore
            </v-btn>

            <v-spacer></v-spacer>

            <v-btn
              icon
            >
            </v-btn>
          </v-card-actions>

        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      courses: [],
      count: 0
    }
  },
  async asyncData({$axios}) {
    const ret = await $axios.$get('/course');
    return {
      courses: ret['data'],
      count: ret['count']
    }
  }
}

</script>

<style scoped>

</style>
