<template>
  <v-app-bar>
    <v-btn>
      <v-icon class="homeButton"> </v-icon>
    </v-btn>
    <v-spacer></v-spacer>
    <v-btn text @click="scoll('home')" class="homeSectoin"> Home </v-btn>
    <v-btn text @click="scoll('Biography')" class="homeSectoin">
      Biography
    </v-btn>
    <v-btn text @click="scoll('Statistics')" class="homeSectoin">
      Statistics
    </v-btn>
  </v-app-bar>
</template>

<style></style>
