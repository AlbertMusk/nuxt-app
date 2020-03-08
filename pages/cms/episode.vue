<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
      <tr>
        <th class="text-left">名称</th>
        <th class="text-left">封面</th>
        <th class="text-left">创建时间</th>
        <th class="text-left">操作</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="item in episodes" :key="item._id">
        <td>{{ item.name }}</td>
        <td><img :src="item['coverUrl']" alt="" width="50"></td>
        <td>{{ item.pubDate }}</td>
        <td>
          <span @click="del(item._id)">删除</span>
          <span @click="edit(item._id)">编辑</span>
        </td>
      </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
  export default {
    name: "episode",
    data() {
      return {
        episodes: []
      }
    },
    async asyncData({$axios}) {
      const ret = await $axios.$get('/episode');
      return {
        episodes: ret['data']
      }
    },
    methods: {
      async del(id) {
        const ret = await this.$axios.$post(`/episode/delete/${id}`);
        if(ret['code'] == 1) {
          console.log(ret['data']);
        }
      }
    }
  }
</script>

<style scoped>

</style>
