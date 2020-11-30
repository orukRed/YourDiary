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
          >
          </v-text-field>
        </v-row>
        <v-row>
          <v-textarea
            label="本文"
            counter="2000"
            color="blue-grey lighten-2"
            maxlength="2000"
          >
          </v-textarea>
        </v-row>
        <v-row>
          <v-col class="text-right">
            <v-btn> 投稿 </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-app>
  </div>
</template>

<script>
export default {
  layout:'MenuBar',  
  data: () => ({
    title: "",
    text: "",
  }),
  methods: {
    postDiary(){

    },
  },

};
</script>