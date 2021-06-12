<template>
  <div class="home">
    <b-container>
      <b-row>
        <b-col sm="12" class="mb-3">
          <h3>ログイン済</h3>
          <hr />
        </b-col>
        <b-col sm="3" class="mx-auto mb-3">
          <b-form-input v-model="id" placeholder="id"></b-form-input>
          <b-form-input v-model="name" placeholder="name"></b-form-input>
        </b-col>
        <b-col sm="12" class="mb-5">
          <b-button variant="primary" v-on:click="postData">登録</b-button>
        </b-col>
        <b-col sm="3" class="mx-auto mb-3">
          <b-table striped hover :items="items"></b-table>
          <b-form-input v-model="text" placeholder="id"></b-form-input>
        </b-col>
        <b-col sm="12" class="mb-5">
          <b-button variant="success" v-on:click="getData">表示</b-button>
          <hr />
        </b-col>
        <b-col sm="12" class="mb-5">
          <!--ログアウトコンポーネント-->
          <amplify-sign-out></amplify-sign-out>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
// API機能読み込み
import { API } from "aws-amplify";

export default {
  name: "home",
  components: {},
  data() {
    return {
      // API Gatewayの名称
      apiName: "api60f15dea",
      //apiName: "1oifsy5t65",
      
      //apiName: "sampleapigateway",
      
      // API Gatewayの設定パス
      path: "/items",
      id: "",
      name: "",
      text: "",
      items: [],
    };
  },
  methods: {
    getData: function () {
      // 検索ID指定
      const path = this.path + "/" + this.text;
      // オプション
      const myInit = {
        headers: {},
        response: true,
      };
      // データ取得
      API.get(this.apiName, path, myInit)
        .then((response) => {
          console.log(response);

          // テーブル表示
          this.items = [
            {
              id: response.data[0].id,
              name: response.data[0].name,
            },
          ];
        });
        //.catch((error) => {
          // テーブルリセット
        //  this.items = [];
        //});
    },
    /*
    postData: function () {
      // オプション
      const myInit = {
        headers: {},
        response: true,
        body: {
          id: Number(this.id),
          name: String(this.name),
        },
      };
      // データ登録
      API.post(this.apiName, this.path, myInit)
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    */
  },
};
</script>
