<template>
  <v-card height="100%" width="100%">
    <v-card-title>{{ title }}</v-card-title>
    <v-divider></v-divider>
    <v-card-text>
      {{ text }}
    </v-card-text>
    <v-divider></v-divider>
    <v-card-actions>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  // propsは親コンポーネントから値渡すときに使う
  props: ["title","text"],
};
</script>