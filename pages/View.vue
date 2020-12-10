<template>
  <div>
    <v-app>
      <v-container>
        <v-row>
          <v-col xs md v-for="(day, key) in days">
            <v-btn @click="fetchTiraura(day)">
              {{ day }}
            </v-btn>
          </v-col>
        </v-row>
        <v-row  v-for="(i, index) in tirauraThumbnail" justify="center">
          <v-col cols=3 v-for ="j in 3">
            <v-btn x-large elevation="8">
              <!-- {{ i["title"] }} -->
              {{ tirauraThumbnail[index+j] }}
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-app>
  </div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/auth";
import "firebase/firestore";
import "date-utils";

export default {
  layout: "MenuBar",
  data: () => ({
    days: ["today", "yesterday"],
    tirauraThumbnail: [],
  }),
  methods: {
    //DBからチラ裏情報取得
    /**
     * @param {string} dt クリックしたのがtodayかyesterdayかを判別
     */
    fetchTiraura(dt) {
      //firebase初期化
      if (!firebase.apps.length) {
        let firebaseApp = firebase.initializeApp(this.$firebaseConfig);
      }

      //日付取得
      let date = new Date();
      let concat = "";

      let today = date.toFormat("YYYYMMDD");
      date.setDate(date.getDate() - 1);
      let yesterday = date.toFormat("YYYYMMDD");

      //クリックしたボタンによって今日or昨日のチラ裏情報取得
      if (dt === "today") {
        concat = today;
      } else if (dt === "yesterday") {
        concat = yesterday;
      }

      //データベースにアクセス
      let db = firebase.firestore();
      let docRef = db
        .collection("scrachPaper" + concat)
        .get()
        .then((snapshot) => {
          snapshot.forEach((doc) => {
            this.tirauraThumbnail.push(doc.data());

            console.log(doc.data());
          });
        })
        .catch((err) => {
          console.log("Error getting documents", err);
        });


      //重複の削除
      this.tirauraThumbnail = this.tirauraThumbnail.filter((x, i, self) => {
        self.indexOf(x) === i; //引数の値で検索
        //selfはthisと同義
      });
    },
  },
};
</script>