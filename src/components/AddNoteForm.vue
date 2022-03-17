<template>
  <div>
    <v-form ref="form" v-model="isValidForm">
      <v-text-field
        v-model="title"
        :rules="titleRules"
        :error-messages="titleErrors"
        :counter="20"
        label="Title"
        required
      ></v-text-field>

      <v-textarea
        v-model="content"
        :rules="contentRules"
        :counter="200"
        clearable
        clear-icon="mdi-close-circle"
        label="Content"
      ></v-textarea>

      <v-select
        v-model="author"
        :rules="authorRules"
        :items="authors"
        label="Author"
        dense
      ></v-select>

      <v-radio-group v-model="isHighImportance">
        <div>Is this note important?</div>
        <v-radio value="1" label="yes"> </v-radio>
        <v-radio value="" label="no"> </v-radio>
      </v-radio-group>

      <div>Add keywors one by one:</div>
      <v-text-field
        v-model="keyword"
        :rules="keywordsRules"
        :error-messages="keywordsErrors"
        :counter="15"
        label="Keyword"
        required
      ></v-text-field>

      <v-btn
        class="mr-4 text-lowercase"
        @click.prevent="addKeyword"
        :disabled="isAddKeywordsButtonDisabled"
      >
        Add new keyword
      </v-btn>
      <div v-if="joinKeywords !== ''" class="mt-3">
        Keywords added: {{ joinKeywords }}.
      </div>

      <v-divider class="my-6"></v-divider>

      <v-btn class="mr-4" @click.prevent="addNewNote" :disabled="!isValidForm">
        <strong>submit</strong>
      </v-btn>
      <v-btn @click="resetForm"> <strong> clear </strong> </v-btn>
    </v-form>

    <v-overlay :value="overlay">
      <v-progress-circular
        indeterminate
        color="green"
        size="50"
        width="8"
      ></v-progress-circular>
    </v-overlay>
  </div>
</template>

<script>
export default {
  name: "AddNoteForm",
  components: {},
  props: {},
  data() {
    return {
      isValidForm: false,
      title: "",
      content: "",
      author: "",
      authors: [],
      isHighImportance: "",
      keyword: "",
      keywordsList: [],
      overlay: false,
      titleRules: [
        (v) => v.length >= 3 || "Minimum length for title is 3 characters",
        (v) => v.length <= 20 || "Maximum length for title is 20 characters",
      ],
      contentRules: [
        (v) => v.length >= 10 || "Minimum length for content is 10 characters",
        (v) =>
          v.length <= 200 || "Maximum length for content is 200 characters",
      ],
      authorRules: [(v) => !!v || "You must choose a name from the list"],
    };
  },

  methods: {
    resetForm() {
      this.title = "";
      this.content = "";
      this.author = "";
      this.isHighImportance = "";
      this.keywordsList = [];
    },

    addNewNote() {
      if (this.$refs.form.validate()) {
        this.$emit(
          "on-click-add-node",
          this.title,
          this.content,
          this.author,
          this.isHighImportance,
          this.keywordsList
        );
        this.resetForm();
      }
    },
    addKeyword() {
      if (this.keyword) {
        this.keywordsList.push(this.keyword);
        this.$emit("on-click-add-keyword", this.keyword);
        this.keyword = "";
      }
    },
    resetValues() {
      this.$emit("on-click-reset");
    },
    emTitle(event) {
      console.log(event);
      this.$emit("update:title", event.target.value);
    },
  },
  computed: {
    joinKeywords() {
      return this.keywordsList.join(", ");
    },
    isAddKeywordsButtonDisabled() {
      if (this.keyword.length < 3 || this.keyword.length > 15) {
        return true;
      }
      return false;
    },
  },

  async created() {
    try {
      this.overlay = true;
      const response = await fetch(
        "https://mocki.io/v1/91c1cd99-8fe0-4eb2-8b42-82c1f940eb01"
      );
      const authorsList = await response.json();
      this.authors = authorsList.map((item) => item.name);
    } catch (err) {
      console.error(err);
    } finally {
      setTimeout(() => {
        this.overlay = false;
      }, 2000);
    }
  },
};
</script>

<style lang="css" computed></style>
