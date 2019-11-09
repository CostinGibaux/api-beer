<template>
  <v-app>
    <v-app-bar
            app
            color="#4286f4"
            dark
    >

      <div class="d-flex align-center">
        <v-container>
          <v-btn href="http://localhost:8080/">
            <v-toolbar-title class="headline text-uppercase">
              <span> Home &nbsp;&nbsp;</span>
            </v-toolbar-title>
          </v-btn>
        </v-container>
      </div>
      <div>
        <v-container>
          <v-btn href="http://localhost:8080/api">
            <v-toolbar-title class="headline text-uppercase">
              <span class="font-weight-bold"> API de bière</span>
            </v-toolbar-title>
          </v-btn>
        </v-container>
      </div>


    </v-app-bar>

    <v-content>
      <router-view/>
    </v-content>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>

<!--



-->