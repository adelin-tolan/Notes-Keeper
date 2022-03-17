<template>
  <v-footer class="success accent-4 white--text">
    <v-container style="max-width: 600px">
      <v-row class="justify-center pt-2">
        <div class="">test@test.com</div>
        <v-icon> mdi-circle-medium </v-icon>
        <div>www.test.com</div>
      </v-row>
      <v-row>
        <v-col>
          <div>
            <v-btn v-for="icon in icons" :key="icon" class="mx-3" dark icon>
              <v-icon size="24px"> mdi-{{ icon }} </v-icon>
            </v-btn>
          </div>
        </v-col>
        <v-col>
          <div>
            ©{{ new Date().getFullYear() }} —
            <strong>Adelin's Notes Keeper</strong>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </v-footer>
</template>

<script>
export default {
  name: "TheFooter",
  data() {
    return {
      icons: ["facebook", "twitter", "linkedin", "github"],
    };
  },
};
</script>

<style lang="css" scoped></style>
