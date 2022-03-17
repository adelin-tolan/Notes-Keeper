<template>
  <v-card class="mx-auto my-2" elevation="2" outlined>
    <v-card-text>
      <p class="text-h6 text--primary">{{ noteTitle }}</p>
      <div class="text--primary">
        {{ noteContent }}
      </div>
      <div>
        <span>{{ noteAuthor }}</span>
        <span>{{ noteDateCreated }}</span>
        <span>
          <v-icon v-if="isHighImportance"> mdi-file-alert </v-icon>
          <v-icon v-else> mdi-file </v-icon>
        </span>
        <span>Keywords: {{ joinKeywords }}.</span>
      </div>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: "NoteItem",
  props: {
    noteTitle: {
      type: String,
      required: true,
    },
    noteContent: {
      type: String,
      required: true,
    },
    noteAuthor: {
      type: String,
      required: true,
    },
    noteDateCreated: {
      type: String,
      required: true,
    },
    isHighImportance: {
      type: Boolean,
      required: true,
    },
    keywords: {
      type: Array,
      required: true,
    },
  },
  computed: {
    joinKeywords() {
      return this.keywords.join(", ");
    },
  },
};
</script>

<style lang="css" scoped>
span {
  display: inline-block;
  margin-right: 10px;
}
</style>
