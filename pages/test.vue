<template>
  <div>
    <p>all：{{ data }}</p>
    <p>1つ目：{{ data.contents[0] }}</p>
    <p>ID：{{ data.contents[0].id }}</p>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, error }) {
    try {
      const res = await $axios.$get("https://bbb.microcms.io/api/v1/blog/", {
        headers: { "X-API-KEY": "b946077c-5861-4db6-bb26-9cf8d183dedf" },
      });
      return {
        data: res,
      };
    } catch (e) {
      error({
        statusCode: 503,
        message: "Unable to fetch events at this time. Please try again.",
      });
    }
  },
};
</script>