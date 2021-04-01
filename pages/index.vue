<template>
  <ul>
    <li v-for="content in contents" :key="content.id">
      <nuxt-link :to="`/${content.id}`">
        {{ content.title }}
      </nuxt-link>
    </li>
  </ul>
</template>

<script>
import axios from 'axios'
export default {
  async asyncData() {
    const { data } = await axios.get(
      'https://bbb.microcms.io/api/v1/blog',
      {
        headers: { 'X-API-KEY': 'b946077c-5861-4db6-bb26-9cf8d183dedf' }
      }
    )
    return data
  }
}
</script>