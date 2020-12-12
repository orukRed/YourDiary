<template>
  <div>
    <v-app>
      <v-container>
        <v-row>
          <v-col xs md v-for="(day, key) in days">
            <v-btn @click="fetchTiraura(day)" color="blue-grey darken-1" dark>
              {{ day }}
            </v-btn>
          </v-col>
        </v-row>
        <v-row v-for="i in tirauraThumbnail">
          <v-col>
            <v-btn
              block
              x-large
              elevation="8"
              @click="fetchTirauraText(i['time'], tirauraThumbnail)"
            >
              {{ i["title"] }}
            </v-btn>
          </v-col>
        </v-row>

        <!-- ダイアログ -->
        <v-row justify="center">
          <!-- v-modelでisDialog=trueのときだけダイアログ表示するようにしている -->
          <v-dialog v-model="isDialog" scrollable max-width="1000px">
            <!-- 特定の条件でポップアップするトリガー用のスロット追加 -->
            <template v-slot:activator="{on}">
              <!-- ポップアップを追加したい要素に対してv=on"on"を追加 -->
              <v-btn color="primary" dark  v-on="on">
                Open Dialog
              </v-btn>
            </template>            
            <!-- ポップアップの内容 -->
            <!-- :があることで:v-bindの短縮形 -->
            <!-- v-bindで属性(propsで指定した名前)名指定して、属性に入れる変数を指定 -->
            <tiraura-text-view :text="text" ></tiraura-text-view>
          </v-dialog>
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
import tirauraTextView from "../components/tirauraTextView.vue";

export default {
  components: { tirauraTextView },
  layout: "MenuBar",
  data: () => ({
    days: ["today", "yesterday"],
    tirauraThumbnail: [],
    isDialog: false,
    text:"",
  }),
  methods: {
    /**
     * 今日の日付をYYYYMMDD形式で取得
     */
    getTodayYYYYMMDD() {
      let date = new Date();
      let today = date.toFormat("YYYYMMDD");
      return today;
    },

    getYesterdayYYYYMMDD() {
      let date = new Date();
      date.setDate(date.getDate() - 1);
      let yesterday = date.toFormat("YYYYMMDD");
      return yesterday;
    },

    /**
     * DBからチラ裏情報取得
     * @param {string} dt クリックしたのがtodayかyesterdayかを判別
     */
    fetchTiraura(dt) {
      //firebase初期化
      if (!firebase.apps.length) {
        let firebaseApp = firebase.initializeApp(this.$firebaseConfig);
      }

      let concat = "";

      //クリックしたボタンによって今日or昨日のチラ裏情報取得
      if (dt === "today") {
        concat = this.getTodayYYYYMMDD();
      } else if (dt === "yesterday") {
        concat = this.getYesterdayYYYYMMDD();
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

    /**
     * ボタン押下されたとき呼ばれる
     * 引数で受け取ったキー(時間)で配列からtextを取得
     * @param {String} keyValue DBに入ってるキー
     */
    fetchTirauraText(keyValue, tiraura) {
      let returnValue  = tiraura.filter((object)=>{
        return object.time == keyValue;  
      }).shift();
      this.text = returnValue.text;
      console.log(this.text);

    },
  },
};
</script>