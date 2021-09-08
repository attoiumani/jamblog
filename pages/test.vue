<template>
  <div>
    <p>all：{{ headerItems }}</p>
    <p>ID：{{ id }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      // APIを叩いて返ってきたコンテンツを格納する用に空の配列を用意
      headerItems: Array,
      id: Array,
    };
  },
  mounted() {
    // mount時にヘッダ一覧を取得する処理を実行
    this.getHeaders();
  },
  methods: {
    getHeaders() {
      // Git管理しないAPIキーは、.envファイル内にて別途定義する
      // オプションとして、コンテンツの最大取得件数は100件と設定
      axios
        .get("https://bbb.microcms.io/api/v1/blog/", {
          headers: { "X-API-KEY": "b946077c-5861-4db6-bb26-9cf8d183dedf" },
        })
        .then((res) => {
          // 取得したコンテンツをコンポーネントのdata内に格納
          this.headerItems = res;
          this.id = res.data.contents[0].id;
          // 取得したアイテムをシャッフル
          for (let i = this.headerItems.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            const tmp = this.headerItems[i];
            this.headerItems[i] = this.headerItems[j];
            this.headerItems[j] = tmp;
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },
    /*
        getHeaders() {
      // Git管理しないAPIキーは、.envファイル内にて別途定義する
      // オプションとして、コンテンツの最大取得件数は100件と設定
      axios
        .get("https://bbb.microcms.io/api/v1/blog/5713hak9-aju", {
          headers: { "X-API-KEY": "b946077c-5861-4db6-bb26-9cf8d183dedf" },
        })
        .then((res) => {
          // 取得したコンテンツをコンポーネントのdata内に格納
          this.headerItems = res;
          this.id = res.data.id;
          // 取得したアイテムをシャッフル
          for (let i = this.headerItems.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            const tmp = this.headerItems[i];
            this.headerItems[i] = this.headerItems[j];
            this.headerItems[j] = tmp;
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },*/ 
  },
};
</script>