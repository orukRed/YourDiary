<template>
  <div>
    <v-app>
      <v-container>
        <v-row>
          <v-text-field
            label="タイトル"
            counter="30"
            hint="最大30文字"
            color="blue-grey lighten-3"
            maxlength="30"
            v-model="title"
          >
          </v-text-field>
        </v-row>
        <v-row>
          <v-textarea
            label="本文"
            counter="2000"
            color="blue-grey lighten-2"
            maxlength="2000"
            v-model="text"
          >
          </v-textarea>
        </v-row>
        <v-row>
          <v-col class="text-right">
            <v-btn @click="postDiary"> 投稿 </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-app>
  </div>
</template>

<script>
// import * as firebase from "firebase/app"; 何故かこっちは通らない
import firebase from "firebase/app";
import "firebase/auth";
import "firebase/firestore";
import "date-utils";

export default {
  layout: "MenuBar",
  data: () => ({
    title: "",
    text: "",
  }),
  methods: {

    postDiary() {
      //日付型
      let time = new Date();


      //firebase初期化
      if (!firebase.apps.length) {
        let firebaseApp = firebase.initializeApp(this.$firebaseConfig);
      }

      let db = firebase.firestore();
      let docRef = db
        .collection("scrachPaper"+time.toFormat("YYYYMMDD"))
        .doc(time.toFormat("HH24:MI:SS")); //引数はそれぞれコレクション名、ドキュメント名
      let setScrachPaper = docRef.set({
        title: this.title,
        text: this.text,
        time: time.toFormat("YYYY/MM/DD HH24:MI:SS"),
      });
      
      //ここに投稿完了のポップアップ入れたいね

      this.title="";
      this.text="";
    },
  },
};
</script>