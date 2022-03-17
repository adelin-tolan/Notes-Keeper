<template>
  <div class="notes-big-container">
    <notes-container></notes-container>
  </div>
</template>

<script>
import NotesContainer from "./NotesContainer.vue";

export default {
  name: "MainNotesContent",
  components: {
    NotesContainer,
  },
};
</script>

<style lang="css" scoped>
.notes-big-container {
  min-height: 80vh;
  margin: 30px 0;
}
</style>
