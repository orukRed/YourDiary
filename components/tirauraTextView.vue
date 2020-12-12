<template>
  <v-card>
    <v-card-title>Select Country</v-card-title>
    <v-divider></v-divider>
    <v-card-text style="height: 300px">
      {{ text }}
    </v-card-text>
    <v-divider></v-divider>
    <v-card-actions>
      <v-btn color="blue darken-1" text @click="isDialog = false">
        Close
      </v-btn>
      <v-btn color="blue darken-1" text @click="isDialog = false"> Save </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  // propsは親コンポーネントから値渡すときに使う
  props: ["text"],
};
</script>