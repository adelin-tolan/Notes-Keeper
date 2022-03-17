<template>
  <div>
    <v-container fluid class="px-0 py-0">
      <v-app-bar color="success accent-4" dark class="py-2">
        <v-row style="max-width: 600px" class="mx-auto">
          <v-img
            max-height="40"
            max-width="40"
            src="../assets/paper-logo.svg"
          ></v-img>

          <v-spacer></v-spacer>

          <v-toolbar-title>Adelin's Notes Keeper</v-toolbar-title>

          <v-spacer></v-spacer>

          <v-btn icon>
            <v-icon>mdi-logout</v-icon>
          </v-btn>
        </v-row>
      </v-app-bar>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "TheHeader",
};
</script>

<style lang="css" scoped></style>
