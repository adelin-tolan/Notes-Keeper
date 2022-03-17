<template>
  <v-app>
    <the-header></the-header>
    <v-main>
      <v-container fluid class="flex">
        <v-row style="max-width: 600px" class="mx-auto mt-6">
          <v-tabs>
            <v-tab @click="handleTabClick('notes')">Notes</v-tab>
            <v-tab @click="handleTabClick('grocery')">Grocery List</v-tab>
          </v-tabs>

          <main-notes-content v-if="main" />
          <main-grocery-list-content v-if="groceryList" />
        </v-row>
      </v-container>
    </v-main>
    <the-footer></the-footer>
  </v-app>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import MainNotesContent from "./components/MainNotesContent.vue";
import TheFooter from "./components/TheFooter.vue";
import MainGroceryListContent from "./components/MainGroceryListContent.vue";

export default {
  name: "App",

  components: {
    TheHeader,
    MainNotesContent,
    MainGroceryListContent,
    TheFooter,
  },

  data() {
    return {
      main: true,
      groceryList: false,
    };
  },
  methods: {
    handleTabClick(tab) {
      if (tab === "notes") {
        this.main = true;
        this.groceryList = false;
      }
      if (tab === "grocery") {
        this.groceryList = true;
        this.main = false;
      }
    },
  },

  computed: {},
};
</script>

<style lang="css" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
