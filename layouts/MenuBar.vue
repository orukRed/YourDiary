<template>
  <div>
    <v-app>
      <header>
        <v-app-bar app color="blue-grey darken-2" dark>
          <v-layout>
            <v-toolbar-title class="text-left font-weight-bold">ここはお前のチラシ裏</v-toolbar-title>
            <v-flex sm class="text-right">
              <v-btn to="/View"> view </v-btn>
              <v-btn to="/write"> write </v-btn>
            </v-flex>
          </v-layout>
        </v-app-bar>
      </header>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    </v-app>
  </div>
</template>
<style>
</style>


<script>
export default {
  data: () => ({}),
  methods: {},
};
</script>