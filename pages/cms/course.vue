<template>
  <div>
    <div class="text-left pa-4">
      <v-btn
        color="success"
        @click="openOverlay"
      >
        新增
      </v-btn>

      <v-overlay :value="show">
        <v-form
          ref="form"
          lazy-validation
          class="col-6"
        >
          <v-text-field
            :counter="10"
            label="Name"
            required
          ></v-text-field>

          <v-text-field
            label="E-mail"
            required
          ></v-text-field>

          <v-btn color="cancel" @click="show = false">取消</v-btn>
          <v-btn color="success">提交</v-btn>
        </v-form>
      </v-overlay>
    </div>

    <v-simple-table>
      <template v-slot:default>
        <thead>
        <tr>
          <th class="text-left">名称</th>
          <th class="text-left">封面</th>
          <th class="text-left">章节</th>
          <th class="text-left">创建时间</th>
          <th class="text-left">操作</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="item in courses" :key="item._id">
          <td>{{ item.name }}</td>
          <td><img :src="item['coverUrl']" alt="" width="50"></td>
          <td><v-select v-model="currentIndex" :items="item.episodes.map((v, i) => ({text: v.name, value: i}))"></v-select></td>
          <td>{{ item.pubDate }}</td>
          <td>
            <v-btn color="error">删除</v-btn>
            <v-btn color="success">编辑</v-btn>
          </td>
        </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>

</template>

<script>
  export default {
    name: "course",
    data() {
      return {
        courses: [],
        currentIndex: 0,
        show: false
      }
    },
    async asyncData({$axios}) {
      const ret = await $axios.$get('/course');
      return {
        courses: ret['data']
      }
    },
    methods: {
      async del(id) {
        const ret = await this.$axios.$get('/course/')
      },
      edit(id) {
        alert(id);
      },
      openOverlay() {
        this.show = true;
      }
    }
  }
</script>

<style scoped>

</style>
