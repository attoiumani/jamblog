<template>
<div>
  <h1>新着</h1>
  <ul>
    <li v-for="content in contents" :key="content.id">
      <nuxt-link :to="`/${content.id}`">
        {{ content.title }}
      </nuxt-link>
    </li>
  </ul>
</div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      contents: Array,
    };
  },
  mounted() {
    this.getHeaders();
  },
  methods: {
     async getHeaders() {
        const res = await this.$axios.$get("https://bbb.microcms.io/api/v1/blog/", {
            headers: { "X-API-KEY": "b946077c-5861-4db6-bb26-9cf8d183dedf" },
          })
        this.contents = res.contents
    },
  },
};

</script>

<style scoped>
ul {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1{
  text-align: center;
}
h1:hover{
  color: rgb(192, 31, 31);
}
</style>