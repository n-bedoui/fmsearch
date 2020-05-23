<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
     
      <v-spacer></v-spacer>
      <v-btn
        href="/map"
        target=""
        text
      >
        <span class="mr-2">My MAp</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>

      <v-spacer></v-spacer>

      <v-btn
        href="/map2"
        target=""
        text
      >
        <span class="mr-2">My MAp2</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>


    <v-content>

       <router-view></router-view>
     
    </v-content>
  </v-app>
</template>

<script>




export default {
  name: 'App',

  data: () => ({
    // les datats
  }),
};
</script>
