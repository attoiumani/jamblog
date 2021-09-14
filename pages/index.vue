<template>
  <div>
    <header />
    <ul>
      <li v-for="content in contents" :key="content.id">
        <nuxt-link :to="`/${content.id}`">
          {{ content.title }}
        </nuxt-link>
      </li>
      <NuxtLink to="/test">apitest</NuxtLink>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import header from "@/components/header";

export default {
  components: {
    header,
  },
  async asyncData() {
    const { data } = await axios.get("https://bbb.microcms.io/api/v1/blog", {
      headers: { "X-API-KEY": "b946077c-5861-4db6-bb26-9cf8d183dedf" },
    });
    return data;
  },
};
</script>